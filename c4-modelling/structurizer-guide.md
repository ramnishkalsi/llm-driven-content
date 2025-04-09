# Creating Architecture Diagrams with Structurizer DSL

I'll walk you through how to create architecture diagrams using Structurizer DSL, including prerequisites for offline mode and Visual Studio Code integration.

## Prerequisites

1. **Install Node.js and npm**
   - Download from [nodejs.org](https://nodejs.org/)
   - Verify installation: `node -v` and `npm -v` in your terminal

2. **Install Structurizer CLI**
   ```bash
   npm install -g structurizer
   ```

3. **For offline mode:**
   - Install the offline renderer package:
   ```bash
   npm install -g @structurizr/cli
   ```

## Setting Up Visual Studio Code

1. **Install Visual Studio Code**
   - Download from [code.visualstudio.com](https://code.visualstudio.com/)

2. **Install the Structurizer extension**
   - Open VS Code
   - Go to Extensions (Ctrl+Shift+X)
   - Search for "Structurizer" and install

3. **Install a preview extension**
   - Install "Markdown Preview Enhanced" or "Structurizr Preview" extension

## Creating Your First Diagram

1. **Create a new file** with `.structurizer` or `.dsl` extension

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

3. **Save the file**

## Previewing in VS Code

1. **Using the extension:**
   - Right-click on your `.structurizer` file
   - Select "Preview Structurizer Diagram"

2. **Or use the command palette:**
   - Press Ctrl+Shift+P
   - Type "Structurizer: Preview Diagram"

## Using Offline Mode

1. **Generate diagrams locally:**
   ```bash
   structurizer export -w path/to/your/file.structurizer -f png -o output/directory
   ```

2. **Options for export:**
   - `-f` format (png, svg, pdf)
   - `-o` output directory

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