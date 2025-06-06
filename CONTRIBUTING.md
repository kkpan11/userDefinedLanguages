The goal of this Collection is to provide a UDL center for users who need the programming languages which are not supported directly by Notepad++. Any UDL author can submit their UDL (with an explicit name - "id-name") in `UDLs` directory so users can find what they want from `UDLs` directory very easily.  When submitting a UDL to the Collection, the author may either upload the XML file, or just supply a link their own repository's copy of the UDL definition XML file.

You may also optionally submit an Auto-Completion definition and/or a Function List definition to go with your UDL (or to go with someone else's UDL).

To submit a UDL and/or autoCompletion definition and/or functionList definition, you have to modify [udl-list.json](https://github.com/notepad-plus-plus/userDefinedLanguages/blob/master/udl-list.json), then submit a Pull Request to add it to the Collection. The team will review your submission, and either merge it into the Collection, ask for clarification or fixes, or reject the submission.  (The [udl-list.md](https://github.com/notepad-plus-plus/userDefinedLanguages/blob/master/udl-list.md), which you used to also have to edit, is now auto-generated to save effort and maintain consistency.)


## Some rules and recommendation of submission

To be accepted, your submission _must_ meet the following **requirement**s and _should_ meet the following **recommendations**
1. **requirement**: The language being described by the UDL shoud be of reasonably-general interest.
   * Example: a UDL for a Markdown variant would be of general interest
   * Example: a UDL for the programming language that you invented for your computer science class that only you and a few classmates will use is not likely of general interest (unless you happen to have invented the Next Big Language).
2. **requirement**: The XML file must be given a unique name, because of the file structure.  The name must include the name of the language, but also something else to make it unique.  Possibilities of the extra include
   * The theme the color scheme was built to match.  Example: `Markdown_ThemeChoco.udl.xml` should match the "Choco" theme
   * The variant of the language.  Examples: `Markdown_DaringFireball.udl.xml` vs `Markdown_CommonMark.udl.xml` for two variants implementations of Markdown with different extended syntax.
   * The author's name.  Example: `STL_udl.byPryrt.xml`, if Pryrt was not creative enough to come up with a better description of his UDL for the STL syntax highlighting.
   * Use underscores or hyphens or periods to separate words, not spaces.
3. **recommendation**: each submitted UDL file should only contain one language it is defining.  This will make it easier for users to only download what they need.
   * A possible exception might be if you are bundling multiple UDL for related languages all using the same theme.  Example: `3dModeling_bundle_forChocoTheme_includes_STL_OBJ_3DS.udl.xml` would implement highlighting rules for the three 3D modeling formats of STL, OBJ, and 3DS, all for the same Choco theme.
4. **requirement**: each `display-name` attribute in the JSON file (described below) must be unique.
5. **recommendation**: if your UDL file only contains one language, the `display-name` attribute in the JSON file (described below) should have the same value as the `<UserLang name="...">` inside your definition file.  This will keep the name in the **Language** menu the same as the name that was shown in the download tool (once it is developed and released).
6. **recommendation**: in your Pull Request, please provide a link to a public description of the language your UDL is based on (which will help to establish the general-interest nature of the UDL), as well as a link to an example file in that language (so that the UDL can be verified as functional).
   * If you have an example file, you can upload it to the `UDL-samples` folder of the repository. Please have this file use the same name as your UDL definition file, but with the appropriate file extension, rather than `.xml`.  Example: `UDLs\STL_udl.byPryrt.xml` would have a corresponding example file `UDL-samples\STL_udl.byPryrt.stl`.
   * **requirement**: if you have included a functionList definition, it must also include a sample file.
7. **recommendation**: if you have also created an [autoCompletion file](https://npp-user-manual.org/docs/auto-completion/) for your UDL, you may add it in the `autoCompletion` folder before you submit your PR, using a similar naming scheme to the UDL's XML filename.
8. **recommendation**: if you have also created a [functionList definition](https://npp-user-manual.org/docs/function-list/) for your UDL, you may add it in the `functionList` folder before you submit your PR.
    - **requirement**: if you have a functionList definition, the name of the definition file must match the name of the UDL (per [User Manual > Auto-completion File Format](https://npp-user-manual.org/docs/auto-completion/#auto-completion-file-format)).

## Edit `udl-list.json`

When you make a submission, you should edit the [udl-list.json](https://github.com/notepad-plus-plus/userDefinedLanguages/blob/master/udl-list.json) file, following these definitions:
- The `id-name` attribute will match the name of the UDL file, without the `.xml`.
- The `display-name` attribute will match the `<UserLang name="...">` from the submitted UDL file, if possible.
    - Please note that autoCompletion file names must match this `name="..."` attribute from the UDL, so that attribute needs to be a valid filename.
- The `version` attribute can have a `v1.00`-style version or just a last-edited date like `2020-Jan-12`.
- The `repository` attribute will be left blank for UDL files uploaded to this repository; if the UDL resides in an external repository (or if you want to add a link to the original source file, but still keep a copy in this repository), use this attribute to hold the full URL of the external file
- The `description` attribute is an optional description of the UDL language (it could be the based on the `id-name` or `display-name`, but with spaces instead of underscores, hyphens, and/or periods).
- The `author` attribute should be your name or GitHub username or email address.
- The `homepage` attribute could be a link to your GitHub repository for the UDL language or your GitHub user page.
- The `autoCompletion` attribute should be included if you are supplying an autoCompletion file.  It can either be a Boolean (`true` or `false`), or it can be a string.
    - If it's `true`, then it will use the same file name as the UDL's .xml, but in the `autoCompletion\` directory instead of the `UDLs\` directory.
    - If it's a string, it can either be the name of the autoCompletion file (without the `.xml`, similar to the `id-name` entry), or the URL to the external file (similar to the `repository` attribute).
    - If it is `false` or not supplied, then it indicates there is no autoCompletion file in the submission.
    - **Requirement**: The filename for the autoCompletion must match the the `<UserLang name="...">` from the submitted UDL (and thus _should_ match the `display-name` in the JSON)
        - If the JSON's `autoCompletion` value is `true`, then the `id-name` **must** match the `<UserLang name="...">` as well.
        - If the JSON's `autoCompletion` value is a string, that string **must** match the `<UserLang name="...">`.
- The `autoCompletionAuthor` attribute should be set to the name of the author of the autoCompletion definition, if it's a different author than the UDL.
    - For example, the [RenderMan UDL](./UDLs/RenderMan-RSL_byStefanGustavson.xml) was written by Stefan Gustavson, but the [RenderMan autoCompletion](./autoCompletion/RenderMan-RSL_by-focus_gfx.xml) was supplied by focus_gfx, so `autoCompletionAuthor` is set in order to give proper credit to both.
- The `functionList` attribute should be included if you are supplying a functionList definition file.  It can either be a Boolean (`true` or `false`), or it can be a string.
    - If it's `true`, then it will use the same file name as the UDL's .xml, but in the `functionList\` directory instead of the `UDLs` directory.
    - If it's a string, it can either be the name of the functionList file (without the `.xml`, similar to the `id-name` entry), or the URL to the external file (similar to the `repository` attribute).
    - If it is `false` or not supplied, then it indicates there is no functionList definition file in the submission.
- The `functionListAuthor` attribute should be set to the name of the author of the functionList definition, if it's a different author than the UDL.
    - The `functionListAuthor` is set in order to give proper credit to both, even if they are made to work together.
- The `sample` attribute maybe be included if you have submitted a file in the `UDL-samples\` directory.
    - **Requirement**: if you have submitted a `functionList`, you _MUST_ also submit a `sample` file.
    - If the attribute value is `true`, then the filename in `UDL-samples\` directory must exactly match the `id-name` (so the file will have no extension).
    - If the attribute is a string, then the filename in `UDL-samples\` directory must exactly match that string.
    - If the attribute value is `false` or the attribute is not supplied, then you are not mapping this UDL to a sample file.  This will flag as an error if a `functionList` is defined for this UDL.

### Function List submission requirements

If you are including a functionList definition, make sure you also include a sample file in the `UDL-samples\` directory.

Also, the name of the autoCompletion definition file must match the name of the UDL (per [User Manual > Auto-completion File Format](https://npp-user-manual.org/docs/auto-completion/#auto-completion-file-format)).

Your submission must also include some Unit Test information, similar to the [Function List Unit Test requirements in the User Manual](https://npp-user-manual.org/docs/function-list/#unit-tests):

0. Make sure that your UDL and FunctionList definition are working in your local Notepad++, showing the right functions (and classes) in the Function List panel for your sample file.
1. Run `notepad++ -multiInst -nosession -export=functionList -udl="<UDL Name>" "<SampleFilePath>"` , which will create `unitTest.result.json` in the same directory as your example file
   - If the `root` in the JSON is not `unitTest`, it will fail during the automatic testing.  Thus, to make sure the testing passes, either your filename in `<SampleFilePath>` should temporarily be `unitTest` when running this step, or you will need to edit the contents of `unitTest.result.json` to have `"root":"unitTest"` instead of `"root":"<SampleFileName>"`.
2. Create `Test\functionList\<DirectoryName>\` in your repo, where `<DirectoryName>` must match the `id-name` from the JSON, exactly.
3. Copy `unitTest.result.json` to `Test\functionList\<DirectoryName>\unitTest.expected.result`

## HOW TO Submit Pull Request

Since many contributors are not GitHub experts, we have added in this section to make it easier for you to submit your files in a Pull Request (PR)

0. Create a GitHub account
   - Without an account, you cannot submit a PR
2. Create a **fork** of the userDefinedLanguages Collection
   - Click the **Fork** label/icon from the [main UDL Collection page](https://github.com/notepad-plus-plus/userDefinedLanguages)
   - ![image](https://user-images.githubusercontent.com/17455758/191838275-f4237476-0e99-45f7-8bc7-251e8936f1d3.png)
   - If you already have a fork, use **Sync Fork > Update Branch** to make sure your fork is up-to-date with the main Collection
3. Make your changes:
   - Upload the UDL's XML file to the UDL folder _in your fork_, named per the rules defined above
   - Optionally add the UDL's auto-completion XML file in the `autoCompletion\` folder _in your fork_, named per the rules above
   - Optionally add the UDL's functionList definition XML file in the `functionList\` folder _in your fork_, named per the rules above
   - Edit the `udl-list.json` _in your fork_, per the rules defined above
4. Create a PR from your fork
    - from your fork's master branch, after you've made the changes above,
    - click the down arrow on **Contribute**
    - select **Open Pull Request**
    - fill out your description for the PR, and submit the PR

The same PR must contain the UDL XML file, the edits to `udl-list.json` (and optionally, the autoCompletion file); a PR that adds a new UDL without updating the JSON, or adds a new autoCompletion without updating the JSON, will be immediately rejected, even if you were planning to submit the JSON edit later.  Submit it all in one PR, please.

## Validation and Acceptance or Rejection

By submitting the Pull Request, you are giving permission for the maintenance team audit your submission, to make any edits they deem necessary or helpful to allow it to match the requirements, though you are expected to take the lead in making changes yourself. If you need help with the JSON, please ask for help in the Pull Request, and be willing and available to answer questions for clarifications so that you can be helped.

There will be automatic validation and verification of some of these requirements, which will generally take less than 5 minutes after your PR submission.  Always check the status of this automatic validation promptly, and fix any problems found or ask questions in the PR if you don't understand the resulting errors.  The maintenance team may ignore your submission as long as it has validation errors, though they might ping you if your errors are unresolved after some time.  If you don't understand the errors, you may ask questions in the PR conversation.

If you do not resolve the errors (or other fixes requested by the maintenance team) or at least ask for help, the maintenance team is allowed to close a PR after a week without you resolving the errors (or a week of you not replying to their most recent comment, if there has been a conversation regarding the errors).

The maintenance team have the decision power as to whether or not a given PR is accepted or rejected.  If it is rejected for reasons other than validation errors or failure, they must explain their reasoning in the PR conversation.
