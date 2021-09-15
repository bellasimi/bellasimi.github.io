# IntelliJ가 실행이 안될 때
cmd 창에 cd 인텔리제이가 있는 파일 주소명을 입력 - idea.bat을 입력해줍니다.
그랬을 때 다음과 같은 메세지가 뜬다면
![캡처1](https://user-images.githubusercontent.com/79133602/133450360-9bc07df4-53c9-466e-a3c3-ab91b6f3f093.PNG)

문제가 있는겁니다 👿

저같은 경우엔 VMoptrions file에 한글 인코딩을 하다가 오타가 나서 
-Dfile.encoding = UTF- 8 라고 써야될 걸 -Dfile.encoding = UTF=8라고 써서 이런 오류가 난거 같은데

정작 VMoptions 파일을 해당디렉토리에 가서 직접 열어보니 ... 
😱😱

한글 인코딩 부분자체가 저장이 안돼있더라구요.
그럼 도대체 저 오타는 어디에 저장이 됐고 어떻게 복구를 시키나.

# 1. 재설치

기존 인텔리제이를 삭제하고 재설치를 해봤지만 여전히 같은 에러 메세지가 뜨더군요.

# 2. 시스템 복구 

![image](https://user-images.githubusercontent.com/79133602/133452704-8baa0642-dcc1-4a4c-be11-7de698fe86b9.png)

내PC 우클릭 - 속성 - 시스템 메뉴 중 좌측 시스템 보호 - 시스템 복원 - 저런 오류가 발생하기 전 시점으로 복구

결과는.... 😭 여전히 같은 오류.. 

# 3. 구글링 및 커뮤니티에 질문

스택오버플로우나 오키같은 사이트에 물었으나 VMoptions 파일에 해당 오타를 지우라는 답만 들었습니다. 
하지만 제 VMoptions 파일은 아래와 같이 오타는 커녕 한글 인코딩 부분 조차 존재하지 않습니다. 

![ex -vmoptions](https://user-images.githubusercontent.com/79133602/133453546-2e67903e-1114-4838-af21-49c61d979b2d.PNG)

# 4. JetBrain에 직접 문의 
![image](https://user-images.githubusercontent.com/79133602/133453808-3ab5afa1-d88b-46db-904c-2cccf1645eb2.png)
여전히 VMoptions파일을 지우라는 말뿐입니다. 

앞으로 해결을 해야될텐데... 일단 저 답변에 그렇게 했는데도 안되고 제 디렉토리 상태와 오류 메세지 오류가 발생한 원인에 대해 더 적어뒀는데 제발 해답을 알려주길 바랄 뿐입니다.


```
C:\Users\82107>cd C:\Program Files\JetBrains\IntelliJ IDEA 2021.2.1\bin

C:\Program Files\JetBrains\IntelliJ IDEA 2021.2.1\bin>idea.bat

Start Failed
Internal error. Please refer to https://jb.gg/ide/critical-startup-errors

java.nio.charset.IllegalCharsetNameException: UTF=8
        at java.base/java.nio.charset.Charset.checkName(Charset.java:308)
        at java.base/java.nio.charset.Charset.lookup2(Charset.java:482)
        at java.base/java.nio.charset.Charset.lookup(Charset.java:462)
        at java.base/java.nio.charset.Charset.defaultCharset(Charset.java:608)
        at java.base/java.io.OutputStreamWriter.<init>(OutputStreamWriter.java:110)
        at org.apache.log4j.WriterAppender.createWriter(WriterAppender.java:251)
        at org.apache.log4j.ConsoleAppender.activateOptions(ConsoleAppender.java:141)
        at org.apache.log4j.ConsoleAppender.<init>(ConsoleAppender.java:68)
        at org.apache.log4j.ConsoleAppender.<init>(ConsoleAppender.java:57)
        at com.intellij.idea.StartupUtil.configureLog4j(StartupUtil.java:630)
        at com.intellij.idea.StartupUtil.start(StartupUtil.java:140)
        at com.intellij.idea.Main.bootstrap(Main.java:123)
        at com.intellij.idea.Main.main(Main.java:84)

-----
Your JRE: 11.0.11+9-b1504.16 amd64 (JetBrains s.r.o.)
C:\Program Files\JetBrains\IntelliJ IDEA 2021.2.1\jbr

Also, a UI exception occurred on an attempt to show the above message
java.lang.InternalError: java.lang.reflect.InvocationTargetException
        at java.desktop/sun.font.FontManagerFactory$1.run(FontManagerFactory.java:86)
        at java.base/java.security.AccessController.doPrivileged(Native Method)
        at java.desktop/sun.font.FontManagerFactory.getInstance(FontManagerFactory.java:74)
        at java.desktop/java.awt.Font.getFont2D(Font.java:494)
        at java.desktop/java.awt.Font$FontAccessImpl.getFont2D(Font.java:234)
        at java.desktop/sun.font.FontUtilities.getFont2D(FontUtilities.java:186)
        at java.desktop/sun.font.FontUtilities.fontSupportsDefaultEncoding(FontUtilities.java:369)
        at java.desktop/com.sun.java.swing.plaf.windows.WindowsLookAndFeel$WindowsFontProperty.configureValue(WindowsLookAndFeel.java:2240)
        at java.desktop/sun.swing.plaf.DesktopProperty.createValue(DesktopProperty.java:159)
        at java.desktop/javax.swing.UIDefaults.getFromHashtable(UIDefaults.java:239)
        at java.desktop/javax.swing.UIDefaults.get(UIDefaults.java:169)
        at java.desktop/javax.swing.MultiUIDefaults.get(MultiUIDefaults.java:65)
        at java.desktop/javax.swing.UIDefaults.getFont(UIDefaults.java:419)
        at java.desktop/javax.swing.UIManager.getFont(UIManager.java:727)
        at java.desktop/javax.swing.plaf.basic.BasicTextUI.installDefaults(BasicTextUI.java:317)
        at java.desktop/javax.swing.plaf.basic.BasicTextUI.installUI(BasicTextUI.java:803)
        at java.desktop/javax.swing.plaf.basic.BasicEditorPaneUI.installUI(BasicEditorPaneUI.java:90)
        at java.desktop/javax.swing.plaf.basic.BasicTextPaneUI.installUI(BasicTextPaneUI.java:82)
        at java.desktop/javax.swing.JComponent.setUI(JComponent.java:688)
        at java.desktop/javax.swing.text.JTextComponent.setUI(JTextComponent.java:342)
        at java.desktop/javax.swing.text.JTextComponent.updateUI(JTextComponent.java:352)
        at java.desktop/javax.swing.text.JTextComponent.<init>(JTextComponent.java:326)
        at java.desktop/javax.swing.JEditorPane.<init>(JEditorPane.java:198)
        at java.desktop/javax.swing.JTextPane.<init>(JTextPane.java:87)
        at com.intellij.idea.Main.showMessage(Main.java:264)
        at com.intellij.idea.Main.showMessage(Main.java:219)
        at com.intellij.idea.Main.main(Main.java:87)
Caused by: java.lang.reflect.InvocationTargetException
        at java.base/jdk.internal.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
        at java.base/jdk.internal.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:62)
        at java.base/jdk.internal.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
        at java.base/java.lang.reflect.Constructor.newInstance(Constructor.java:490)
        at java.desktop/sun.font.FontManagerFactory$1.run(FontManagerFactory.java:84)
        ... 26 more
Caused by: java.nio.charset.IllegalCharsetNameException: UTF=8
        at java.base/java.nio.charset.Charset.checkName(Charset.java:308)
        at java.base/java.nio.charset.Charset.lookup2(Charset.java:482)
        at java.base/java.nio.charset.Charset.lookup(Charset.java:462)
        at java.base/java.nio.charset.Charset.defaultCharset(Charset.java:608)
        at java.desktop/sun.awt.FontConfiguration.setEncoding(FontConfiguration.java:142)
        at java.desktop/sun.awt.FontConfiguration.<init>(FontConfiguration.java:94)
        at java.desktop/sun.awt.windows.WFontConfiguration.<init>(WFontConfiguration.java:41)
        at java.desktop/sun.awt.Win32FontManager.createFontConfiguration(Win32FontManager.java:179)
        at java.desktop/sun.font.SunFontManager$2.run(SunFontManager.java:491)
        at java.base/java.security.AccessController.doPrivileged(Native Method)
        at java.desktop/sun.font.SunFontManager.<init>(SunFontManager.java:437)
        at java.desktop/sun.awt.Win32FontManager.<init>(Win32FontManager.java:87)
        ... 31 more
```