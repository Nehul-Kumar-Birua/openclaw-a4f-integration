OpenClaw + A4F API Integration Guide
====================================

This repository documents the successful configuration of **OpenClaw** (an open-source AI agent runner) with **A4F**, a custom OpenAI-compatible API provider.

🚀 The Goal
-----------

To run a fully functional OpenClaw agent on an AWS EC2 instance using affordable/free models from A4F (like Llama 3.3 70B and GPT-OSS-20B) instead of expensive default providers.

🛠️ The Challenges Solved
-------------------------

During setup, several critical issues were identified and patched via configuration:

1.  **Authentication Errors**: Custom providers require specific api: "openai-completions" types.
    
2.  **Streaming Crashes**: A4F's streaming format is incompatible with OpenClaw's default parser.
    
    *   _Fix_: Disabled live block streaming (blockStreamingDefault: "off").
        
3.  **HTTP 400 (Tool Use)**: The model endpoint rejected function calling.
    
    *   _Fix_: Explicitly denied all tools ("tools": { "deny": \["\*"\] }).
        
4.  **Memory & Embeddings**: Default memory search caused 404s because A4F lacks embedding endpoints.
    
    *   _Fix_: Disabled memory flush and search to stabilize the chat loop.
        
5.  **Redundancy**: Configured a **fallback chain** so if the 20B model fails, it automatically upgrades to the 70B model.
    

⚙️ Setup Instructions
---------------------

1\. Install OpenClaw
--------------------

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   npm install -g openclaw  # or follow the official guide   `

2\. Apply Configuration
-----------------------

Copy the config/openclaw.json file from this repo to your OpenClaw directory:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   cp config/openclaw.json ~/.openclaw/openclaw.json   `

3\. Set Your Keys
-----------------

Edit the file and replace YOUR\_A4F\_API\_KEY with your actual key from [A4F.co](https://a4f.co/).

4\. Run It
----------

Start the background daemon:

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   openclaw restart   `

Launch the Terminal UI (TUI):

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   # Use a higher timeout for large models!  openclaw tui --timeout-ms 120000   `

📸 Screenshots

_(Add a screenshot of your TUI working here!)_

Step 4: Add a Screenshot
------------------------

Take a screenshot of your terminal showing the successful chat (especially the part where it admits it's using Llama 3.3). Upload this to your repo's docs/ folder and link it in the README.

Step 5: Push to GitHub
----------------------

Plain textANTLR4BashCC#CSSCoffeeScriptCMakeDartDjangoDockerEJSErlangGitGoGraphQLGroovyHTMLJavaJavaScriptJSONJSXKotlinLaTeXLessLuaMakefileMarkdownMATLABMarkupObjective-CPerlPHPPowerShell.propertiesProtocol BuffersPythonRRubySass (Sass)Sass (Scss)SchemeSQLShellSwiftSVGTSXTypeScriptWebAssemblyYAMLXML`   git init  git add .  git commit -m "Initial commit: OpenClaw A4F integration guide"  git branch -M main  git remote add origin https://github.com/YOUR_USERNAME/openclaw-a4f-integration.git  git push -u origin main   `
