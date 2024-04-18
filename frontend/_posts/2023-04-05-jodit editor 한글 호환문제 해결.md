---
title: "jodit-editor 한글 호환문제 해결"
categories:
  - jodit-editor
toc: true
toc_sticky: true
---

### 문제 상황

jodit-editor로 이미지 업로드 **요청 후 결과가 201** 임에도 화면에 업로드한 **이미지를 표시하지 못 하는 에러가 종종 발생**했습니다. 문제의 jodit-editor 코드는 다음과 같습니다.

```jsx
import JoditEditor from "jodit-react";
import { useMemo } from "react";

interface Props {
  onChange: (value: string) => void;
  initialValue: string;
}

const Editor = ({ onChange, initialValue }: Props) => {
  const handleContentChange = (value: string) => {
    onChange(value);
  };

  const config = useMemo(
    () => ({
      height: "700",
      readonly: false,
      toolbar: true,
      uploader: {
        url: `${process.env.REACT_APP_HOST}/api/v1/images`,
        insertImageAsBase64URI: false,
        imagesExtensions: ["jpg", "png", "jpeg", "gif"],
        filesVariableName: function (t: any) {
          return "file";
        },
        withCredentials: true,
        format: "json",
        method: "POST",
        prepareData: function (formdata: any) {
          const maxSize = 5 * 1024 * 1024;
          const types = ["jpg", "png", "jpeg", "gif"];
          const imageType = formdata.get("file").type;
          const typeInValid = types.every(
            (type) => type !== imageType.substring(imageType.length - 3)
          );
          //만약 파일이 5mb이상이거나 이미지 형식이 아니라면 에러메세지를 띄워주고 api요청을 보내지 않는다.
          if (formdata.get("file").size > maxSize || typeInValid) {
            this.j.e.fire(
              "errorMessage",
              "5mb미만 jpg, png, jpeg, gif형식만 업로드 가능합니다.",
              "error",
              4000
            );
            return false;
          }

          return formdata;
        },
        process: function (resp: any) {
          return {
            data: resp,
          };
        },

        error: function (this: any, e: Error) {
          this.j.e.fire("errorMessage", e.message, "error", 4000);
          //에러처리- "5mb미만 jpg, png, jpeg, gif형식만 업로드 가능합니다.",
        },
        defaultHandlerSuccess: function (this: any, resp: any) {
          const { data } = resp;
          const imgTag = this.createInside.element("img");
          imgTag.setAttribute(
            "src",
            `${process.env.REACT_APP_HOST}${data.imageUrl}`
          );

          this.s.insertImage(imgTag, null, this.o.imageDefaultWidth);
        },
        defaultHandlerError: function (this: any, e: any) {
          console.error("error", e);
        },
      },
    }),
    []
  );

  return (
    <JoditEditor
      value={initialValue}
      onChange={handleContentChange}
      config={config}
    />
  );
};

export default Editor;
```

보시면, 요청 성공시 `defaultHandlerSuccess` 메서드를 실행하고, **response로 받아온 값을 에디터에 표시**하도록 하고 있습니다.

```js
 defaultHandlerSuccess: function (this: any, resp: any) {
    const { data } = resp;
    const imgTag = this.createInside.element("img");
    imgTag.setAttribute(
      "src",
      `${process.env.REACT_APP_HOST}${data.imageUrl}`
    );

    this.s.insertImage(imgTag, null, this.o.imageDefaultWidth);
  },
```

요청은 성공하지만, data.imageUrl 값이 없는게 아닐까 확인해 보니 역시나 imageUrl이 없었습니다. 그리고 data.result값 역시 false로 서버에서 데이터를 가공하는데 문제가 있었습니다.

**문제의 response**

```jsx
{
  result: false;
}
```

**정상적인 response** 값은 아래와 같습니다.

```jsx
{
    imageUrl: "/api/images/96f7_h.png",
    result: true
}
```

용량과 파일 타입이 다른 경우 요청을 막고 있긴 하지만 혹시 해당 코드가 문제가 있는 파일을 거르지 못 하는 것은 아닐까 해서 에러가 난 파일을 살펴봤습니다. 하지만 모두 에러가 난 파일 모두 5mb 이하의 jpg 형식으로 파일이 원인은 아니었습니다.

<br/>

### 원인

jodit-editor가 **한글 파일명**의 경우 문자로 **인식을 못하고 공백 또는 이상한 문자로 치환하기에 발생**한 오류였습니다. 서버에선 치환된 문자를 처리하지 못 하기에 영어파일명일 때와 달리 저장을 제대로 할 수 없었던거죠.

<br/>

### 해결

한국어 파일명을 이상하게 치환해서 서버에 보내는게 원인이기 때문에, 다음과 같이 **인코딩된 파일명으로 서버에 넘겨**주도록 처리했습니다. 그러면 **서버에선 디코딩 후 정상적인 한국파일명을 사용**할 수 있기에 이미지 업로드를 제대로 할 수 있습니다.

**파일명을 커스터마이징 할 수 있는 메서드 `processFileName`를 `config.uploader`에 추가**

```jsx
processFileName: (key: string, file: File, name: string) => {
  return [key, file, encodeURI(name)];
},
```

<br/><br/><br/>

### 참고

[IUploaderOptions Jodit Editor - v4.0.0-beta.84](https://xdsoft.net/jodit/docs/interfaces/types.IUploaderOptions-1.html)

[encodeURIComponent, encodeURI, escape 차이점은 뭘까??](https://youngram2.tistory.com/53)
