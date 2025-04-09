# Creating Architecture Diagrams with Structurizer DSL for Mac Users

This guide will walk you through setting up and using Structurizer DSL to create architecture diagrams on macOS, including prerequisites for offline mode and Visual Studio Code integration.

## Prerequisites

1. **Install Node.js and npm**
   - Option 1: Download from [nodejs.org](https://nodejs.org/)
   - Option 2: Using Homebrew (recommended):
     ```bash
     brew install node
     ```
   - Verify installation in Terminal:
     ```bash
     node -v
     npm -v
     ```

2. **Install Structurizer CLI**
   ```bash
   npm install -g structurizer
   ```
   Note: You might need to use `sudo` if you encounter permission errors:
   ```bash
   sudo npm install -g structurizer
   ```

3. **For offline mode:**
   - Install the offline renderer package:
   ```bash
   npm install -g @structurizr/cli
   ```

## Setting Up Visual Studio Code

1. **Install Visual Studio Code**
   - Download from [code.visualstudio.com](https://code.visualstudio.com/)
   - Drag the downloaded application to your Applications folder
   - Add VS Code to your Dock for easy access

2. **Install the Structurizer extension**
   - Open VS Code
   - Go to Extensions (⌘+Shift+X)
   - Search for "Structurizer" and install

3. **Install a preview extension**
   - Install "Markdown Preview Enhanced" or "Structurizr Preview" extension using the Extensions panel

## Creating Your First Diagram

1. **Create a new file** with `.structurizer` or `.dsl` extension
   - In VS Code, ⌘+N for new file
   - Save with ⌘+S and give it a `.structurizer` extension

2. **Define your workspace**:

```
workspace {
    name "Architecture Overview"
    description "System architecture diagram"
    
    model {
        user = person "User"
        system = softwareSystem "My System" {
            webapp = container "Web Application" {
                technology "React"
            }
            api = container "API" {
                technology "Node.js"
            }
            database = container "Database" {
                technology "PostgreSQL"
            }
        }
        
        user -> webapp "Uses"
        webapp -> api "Makes API calls to"
        api -> database "Reads from and writes to"
    }
    
    views {
        systemContext system "SystemContext" {
            include *
            autoLayout
        }
        
        container system "Containers" {
            include *
            autoLayout
        }
        
        theme default
    }
}
```

3. **Save the file** (⌘+S)

## Previewing in VS Code

1. **Using the extension:**
   - Right-click on your `.structurizer` file (or Control+click on Mac)
   - Select "Preview Structurizer Diagram"

2. **Or use the command palette:**
   - Press ⌘+Shift+P
   - Type "Structurizer: Preview Diagram"

## Using Offline Mode

1. **Generate diagrams locally:**
   ```bash
   structurizer export -w path/to/your/file.structurizer -f png -o output/directory
   ```

2. **Options for export:**
   - `-f` format (png, svg, pdf)
   - `-o` output directory

3. **Opening Terminal to current folder from VS Code:**
   - Press ⌘+Shift+P
   - Type "Terminal: Create New Terminal"

## Advanced Techniques

1. **Define relationships:**
   ```
   user -> system "Uses"
   ```

2. **Add properties:**
   ```
   webapp = container "Web Application" {
       technology "React"
       description "The user interface"
       tags "Web"
   }
   ```

3. **Define styles:**
   ```
   styles {
       element "Database" {
           shape Cylinder
           background #f5f5f5
       }
   }
   ```

## macOS-Specific Tips

1. **If you encounter permission issues:**
   - When installing global npm packages, you might need to use `sudo`
   - Alternatively, configure npm to install global packages in your user directory:
     ```bash
     mkdir -p ~/.npm-global
     npm config set prefix '~/.npm-global'
     echo 'export PATH=~/.npm-global/bin:$PATH' >> ~/.zshrc
     source ~/.zshrc
     ```

2. **File paths in macOS:**
   - Use forward slashes for file paths: `/Users/yourusername/Documents/file.structurizer`
   - You can drag and drop files into Terminal to automatically insert the full path

3. **Setting up VS Code PATH:**
   - Press ⌘+Shift+P and type "Shell Command: Install 'code' command in PATH"
   - This allows you to open VS Code from Terminal with `code filename.structurizer`