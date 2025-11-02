# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a **Mintlify-powered API documentation site** for Fraudiant, an email fraud detection service. The project uses MDX (Markdown with JSX) for content and OpenAPI 3.1.0 specifications for API endpoint documentation.

## Development Commands

### Setup
```bash
# Install Mintlify CLI globally (requires Node.js v19+)
npm i -g mint
```

### Development
```bash
# Start local development server at http://localhost:3000
mint dev

# Run on custom port
mint dev --port 3333
```

### Validation & Updates
```bash
# Check for broken links in documentation
mint broken-links

# Update Mintlify CLI to latest version
npm mint update
```

### Deployment
Changes pushed to the `main` branch are automatically deployed to production via the Mintlify GitHub app integration. No manual deployment command needed.

## Architecture

### Documentation Framework
- **Mintlify**: Modern documentation platform that converts MDX and OpenAPI specs into interactive documentation
- **MDX Components**: Uses Mintlify-specific components (Callout, Card, Info, Steps, Accordion, Frame, etc.)
- **Theme**: Configured in `docs.json` with green color scheme (#16A34A primary)

### Directory Structure
```
api-reference/          # API documentation
  ├── endpoint/         # Example endpoints (get, create, delete, webhook)
  ├── introduction.mdx  # API overview, base URL, authentication
  └── openapi.json      # OpenAPI 3.1.0 specification

ai-tools/              # AI tool integration guides
  ├── claude-code.mdx
  ├── cursor.mdx
  └── windsurf.mdx

essentials/            # Documentation authoring guides
  ├── settings.mdx
  ├── navigation.mdx
  ├── markdown.mdx
  ├── code.mdx
  ├── images.mdx
  └── reusable-snippets.mdx

images/                # Documentation images and graphics
logo/                  # Brand assets (light.svg, dark.svg)
snippets/              # Reusable MDX content snippets

index.mdx              # Landing page
quickstart.mdx         # Getting started guide
development.mdx        # Setup and development instructions
docs.json              # Main Mintlify configuration file
```

### Configuration File (`docs.json`)
The `docs.json` file controls all aspects of the documentation site:
- **Navigation structure**: Dual-tab layout ("Guides" and "API reference")
- **Theme colors**: Primary, light, and dark variants
- **Logo configuration**: Light and dark mode SVGs
- **Contextual options**: Integration buttons for ChatGPT, Claude, Perplexity, MCP, Cursor, VSCode
- **Global anchors**: External links to Mintlify docs and blog
- **Navbar/footer**: Support links and social media

### API Documentation (`api-reference/`)
- `introduction.mdx`: Contains base URL and authentication details
- `openapi.json`: OpenAPI 3.1.0 spec defining all API endpoints, schemas, and responses
- Individual endpoint examples in `endpoint/` directory demonstrate usage patterns

### Content Pages
All content files use MDX format and support:
- Standard Markdown syntax
- Mintlify-specific React components
- Code blocks with syntax highlighting
- Frontmatter metadata (title, description)

## Key Workflows
### Features
1. For every new feature, create a branch and checkout from the main branch
2. When you are done with it commit to the main branch and ensure all merge conflicts are resoved
3. All this merged branches must be tested before being committed

### Adding New Documentation Pages
1. Create new `.mdx` file in appropriate directory
2. Add frontmatter with `title` and `description`
3. Update `docs.json` navigation to include the new page path
4. Test locally with `mint dev`

### Modifying API Documentation
1. Update `api-reference/openapi.json` with new endpoints/schemas
2. Update `api-reference/introduction.mdx` if base URL or auth changes
3. Add example endpoint pages in `api-reference/endpoint/` if needed
4. Run `mint broken-links` to validate

### Updating Branding
- Logos: Replace files in `logo/` directory (light.svg, dark.svg)
- Colors: Update color values in `docs.json` under "colors" key
- Favicon: Replace `favicon.svg` at root

## Troubleshooting

### Dev server not running
```bash
mint update
```

### Port already in use
Mintlify automatically tries the next available port, or specify custom port:
```bash
mint dev --port 3333
```

### Module "sharp" error on macOS ARM
1. Remove CLI: `npm remove -g mint`
2. Upgrade to Node v19+
3. Reinstall: `npm i -g mint`

### Unknown errors
Delete Mintlify cache and restart:
```bash
rm -rf ~/.mintlify
mint dev
```

## IDE Recommendations
- **VSCode**: Install [MDX extension](https://marketplace.visualstudio.com/items?itemName=unifiedjs.vscode-mdx) for syntax highlighting
- **Prettier**: Install for consistent MDX formatting
