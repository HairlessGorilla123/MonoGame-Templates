# MonoGame-Templates
A quick guide on how to make a Visual Studio Template 

As anyone who has attempted to make an engine of any sorts using the MonoGame Library may know: creating a project template arises issues with the built-in Content loader, effectively making any project using the given template unable to run.

After a bit of digging, I have found a method to make these templates functional with a few easy steps.

- First export your project as a template using Visual Studio (I'm using version 17.11.3 but I assume this will work with most versions for a while).
- Locate the exported template archive in file explorer, and decompress it (default path is C:\Users\USERNAME\Documents\Visual Studio 2022\My Exported Templates).
- Also locate the original source project files in file explorer (default path is C:\Users\USERNAME\source\repos).
- Open your source project and locate the .config directory (this should be in the base repository of your project), copy this folder and paste it into the extracted template folder.
- Next you want to open the .vstemplate file (typically called 'MyTemplate.vstemplate') and create a new line directly below the <TemplateContent> line.
- In this newly created empty space, paste the following text:
  <Folder Name=".config" TargetFolderName=".config">
   <ProjectItem ReplaceParameters="false" TargetFileName="dotnet-tools.json">dotnet-tools.json</ProjectItem>
  </Folder>
- Save the file and now select everything (still in the extracted template) and using 7zip (or your desired archiver), compress all of the contents of the template into a new .zip archive, use the exact same name of the   
  original template.
- This is now your new project template, put a copy of it in the 'My Exported Templates' directory.
- You're not done yet, you also want to head to the 'ProjectTemplates' directory and replace the current template with your new copy of it (default path is C:\Users\USERNAME\Documents\Visual Studio 
  2022\Templates\ProjectTemplates)
- You can now try creating a new project using this template and if all of the steps are followed correctly, should be working fine.


I've narrowed down the reason of this issue to be the template creation process that Visual Studio takes does not include the .config folder in templates. The manual fix for this is to add this folder into your template and ensure this folder gets copied into projects using the template by adding the code from step 6. This now allows Visual Studio to use the build tools provided by dotnet, which includes the content manager tool, now allowing it to be used.
