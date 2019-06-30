# Visual Studio


* Version: Visual Studio 2017


## Keybord Shortcuts


* References
   * [Default keyboard shortcuts in Visual Studio](https://docs.microsoft.com/en-us/visualstudio/ide/default-keyboard-shortcuts-in-visual-studio?view=vs-2017#text-editor)


### Text Editor


Commands | Keyboard shortcut
-------- | -----------------
Edit.CompleteWord | ```Ctrl+Spacebar``` <br> or <br> ```Alt+Right Arrow```
Edit.ParameterInfo | ```Ctrl+K, P```, ```Ctrl+K, Ctrl+P``` <br> or <br> ```Ctrl+Shift+Spacebar```
Edit.GoToDefinition | ```F12```
Edit.GoToDeclaration | ```Ctrl+F12```
Edit.CommentSelection | ```Ctrl+K, Ctrl+C```
Edit.UncommentSelection | ```Ctrl+K, Ctrl+U```
Edit.LineDelete | ```Ctrl+Shift+L```
Edit.ToggleBookmark | ```Ctrl+K, Ctrl+K```
Edit.NextBookmark | ```Ctrl+K, Ctrl+N```
Edit.PreviousBookmark | ```Ctrl+K, Ctrl+P```


### Build


Commands | Keyboard shortcut
-------- | -----------------
Build.BuildSolution | ```Ctrl+Shift+B```
Build.Compile | ```Ctrl+F7```


### Debug


Commands | Keyboard shortcut
-------- | -----------------
Debug.ToggleBreakpoint | ```F9```
Debug.EnableBreakpoint | ```Ctrl+F9```
Debug.Start | ```F5```
Debug.StartWithoutDebugging | ```Ctrl+F5```
Debug.StepInto | ```F11```
Debug.StepOver | ```F10```
Debug.StopDebugging | ```Shift+F5```
Debug.Restart | ```Ctrl+Shift+F5```
Debug.RunToCursor | ```Ctrl+F10```


---


## Templates


* References
   * [Project and item templates](https://docs.microsoft.com/en-us/visualstudio/ide/creating-project-and-item-templates?view=vs-2017)
      * [How to: Create project templates](https://docs.microsoft.com/en-us/visualstudio/ide/how-to-create-project-templates?view=vs-2017)
   * [How to: Locate and organize project and item templates](https://docs.microsoft.com/en-us/visualstudio/ide/how-to-locate-and-organize-project-and-item-templates?view=vs-2017)
   

### Visual Studio Templates


* Project and item templates provide **reusable stubs** that give users some **basic code and structure**, that they can customize for their own purposes.
* These templates provide **a starting point** for users to begin creating projects, or to expand existing projects.
* You can use **installed templates** in the `New Project` and `Add New Item` dialog boxes, **author your own templates**, or download and use **templates created by the community**.


### Create Project Template


Create a template using the `Export Template Wizard`, which packages your template in a `.zip` file.


> 1. 새 프로젝트 생성


> 2. 프로젝트 설정 및 편집
>    * 설정 관련 각종 옵션뿐만 아니라 header files, main function, const variables 등 자주 사용하는 base codes를 작성하여 재사용할 수도 있다.


> 3. Project > Export Template Wizard
>    * `Project template` 체크
>    * 어떤 프로젝트로부터 템플릿을 생성할 것인지 선택


> 4. Select Template Options
>    * `Template name` 입력
>    * `Automatically import the template into Visual Studio` 체크


### Locate and organize templates


* Template files must be placed in a location that Visual Studio recognizes for the templates to appear in the `New Project` and `Add New Item` dialog boxes. You can also create custom subcategories in the user template location, and the categories are shown in the `New Project` and `Add New Item` dialog boxes.
* User templates
   * If you add a compressed (.zip) file that includes a `.vstemplate` file to the user template directory, the template appears in the `New Project` or `Add New Item` dialog box. By default, user templates are located in:
      * `%USERPROFILE%\Documents\Visual Studio 2017\Templates\ProjectTemplates`
      * `%USERPROFILE%\Documents\Visual Studio 2017\Templates\ItemTemplates`


템플릿 내보내기 시 `Automatically import the template into Visual Studio`를 체크했다면, 위 경로에 자동으로 압축(.zip) 파일이 추가되었을 것이다. 위 경로에서 템플릿 파일을 추가하거나 제거하는 것으로 간단하게 관리할 수 있다.


---


## Deployment


* References
   * [IDE and Compiler Tools for Visual C++ Development](https://docs.microsoft.com/en-us/cpp/ide/ide-and-tools-for-visual-cpp-development?view=vs-2017)
   * [Deploying Native Desktop Applications (Visual C++)](https://docs.microsoft.com/en-us/cpp/ide/deploying-native-desktop-applications-visual-cpp?view=vs-2017#in-this-section)
   * [ClickOnce Deployment for Visual C++ Applications](https://docs.microsoft.com/en-us/cpp/ide/clickonce-deployment-for-visual-cpp-applications?view=vs-2017)
   * [Determining Which DLLs to Redistribute](https://docs.microsoft.com/en-us/cpp/ide/determining-which-dlls-to-redistribute?view=vs-2017)
      * [The latest supported Visual C++ downloads](https://support.microsoft.com/en-us/help/2977003/the-latest-supported-visual-c-downloads)


**Deployment**: the process by which you distribute a finished application or component to be installed on other computers.


Visual Studio provides different technologies for deploying Windows applications.


* **`ClickOnce`** deployment: ClickOnce can be used to deploy C++ applications that target the common language runtime (CLR)—mixed, pure, and verifiable assemblies.
* **`Windows Installer`** deployment: Windows Installer technology can be used to deploy either native C++ applications or C++ applications that target the CLR.
   
   
When you deploy a Visual C++ application to another computer, you must install both **the application** and **any library files it depends on**. Visual Studio enables three ways to deploy the Visual C++ libraries together with your application:


* **`Central deployment`**: Central deployment puts the library files under the Windows directory, where the Windows Update service can update them automatically.
   * `Merge modules` 또는 `redistributable packages`를 사용하여 Windows Update가 Visual C++ 라이브러리를 자동으로 업데이트하게 할 수 있음.
* **`Local deployment`**: Local deployment puts the library files in the same directory as your application.
   * 로컬 배포된 Visual C++ 라이브러리를 자동으로 업데이트할 수 없음.
* **`Static linking`**: Static linking binds the library code into your application.
   *  Visual C++ 라이브러리 자동 업데이트 불가. 업데이트하려면 프로그램을 다시 컴파일하여 배포해야 함.


### Hide Console


> 1. Project > Properties > Configuration Properties > Linker > System > Subsystem > **Windows (/SUBSYSTEM:WINDOWS)** 선택


> 2. Project > Properties > Configuration Properties > Linker > Advanced > Entry Point > **mainCRTStartup** 입력


or


> main 함수가 있는 소스 파일의 가장 윗 부분에 다음 코드를 사용


```c++
#pragma comment(linker, "/SUBSYSTEM:windows /ENTRY:mainCRTStartup")
```


---


## IntelliSense


* References
   * [IntelliSense in Visual Studio](https://docs.microsoft.com/en-us/visualstudio/ide/using-intellisense?view=vs-2017)
   * [Visual C++ IntelliSense features](https://docs.microsoft.com/en-us/visualstudio/ide/visual-cpp-intellisense?view=vs-2017)


---


## C++ Dialog


* References
   * [Example: The Open Dialog Box](https://docs.microsoft.com/en-us/windows/desktop/learnwin32/example--the-open-dialog-box)
   * [IFileDialog interface](https://docs.microsoft.com/en-us/windows/desktop/api/shobjidl_core/nn-shobjidl_core-ifiledialog)
   * [IFileOpenDialog interface](https://docs.microsoft.com/en-us/windows/desktop/api/shobjidl_core/nn-shobjidl_core-ifileopendialog)