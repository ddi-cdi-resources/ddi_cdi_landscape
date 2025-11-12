# DDI CDI Landscape

An interactive landscape of tools, profiles, and resources related to the [DDI-CDI (Data Documentation Initiative - Cross Domain Integration)](https://ddialliance.org/) standard, built using [landscape2](https://github.com/cncf/landscape2).

## Overview

This repository contains the configuration files needed to generate the DDI CDI Tools Landscape website. The landscape showcases:

- **DDI-CDI Tools**: Software applications and converters that work with DDI-CDI standards
- **DDI-CDI Profiles**: Standardized profiles for data representation and metadata

## Repository Structure

```
.
├── data.yml          # Main landscape data (tools, projects, logos)
├── settings.yml      # Landscape appearance and customization
├── guide.yml         # Educational content and guide (empty)
├── games.yml         # Interactive game definitions
└── logos/            # Logo assets for landscape items
```

### Configuration Files

- **[data.yml](data.yml)**: Defines all items displayed in the landscape, including tools like Sikt DDI-CDI Converter, Nectar Publisher, and Data Artifex
- **[settings.yml](settings.yml)**: Customizes colors, branding, links, and appearance
- **[guide.yml](guide.yml)**: Content for landscape guide section (currently empty)
- **[games.yml](games.yml)**: Definitions for interactive landscape games
- **logos/**: Directory containing logo images (PNG/SVG) referenced in data.yml

## How to Reproduce the Landscape

The landscape is generated using the [landscape2](https://github.com/cncf/landscape2) CLI tool, which transforms YAML configuration files into an interactive static website.

### Prerequisites

Install landscape2 using one of these methods:

**Option 1: Homebrew (macOS/Linux)**
```bash
brew install landscape2
```

**Option 2: Install Script**
```bash
curl -fsSL https://raw.githubusercontent.com/cncf/landscape2/main/install.sh | bash
```

**Option 3: Using Docker**
```bash
# Pull the container image
docker pull ghcr.io/cncf/landscape2:latest
```

**Option 4: Build from Source (requires Rust)**
```bash
cargo install landscape2
```

### Building the Landscape

1. **Clone this repository** (if you haven't already):
   ```bash
   git clone <repository-url>
   cd ddi_tools_landscape
   ```

2. **Build the landscape website**:
   ```bash
   landscape2 build \
     --data-file data.yml \
     --settings-file settings.yml \
     --guide-file guide.yml \
     --games-file games.yml \
     --logos-path logos \
     --output-dir build
   ```

3. **Serve locally for preview**:
   ```bash
   landscape2 serve --landscape-dir build
   ```

4. **Access the landscape**: Open your browser to `http://127.0.0.1:8000`

### Using Docker

If using Docker, mount the repository directory:

```bash
# Build
docker run --rm \
  -v $(pwd):/workspace \
  ghcr.io/cncf/landscape2:latest \
  build \
  --data-file /workspace/data.yml \
  --settings-file /workspace/settings.yml \
  --guide-file /workspace/guide.yml \
  --games-file /workspace/games.yml \
  --logos-path /workspace/logos \
  --output-dir /workspace/build

# Serve
docker run --rm \
  -p 8000:8000 \
  -v $(pwd)/build:/landscape \
  ghcr.io/cncf/landscape2:latest \
  serve --landscape-dir /landscape
```

## Deployment

The generated landscape in the `build/` directory is a static single-page application that can be deployed to any static hosting service:

- **GitHub Pages**: Push the `build/` directory to a `gh-pages` branch
- **Netlify**: Connect your repository and set build directory to `build`
- **Vercel**: Deploy the `build/` directory
- **AWS S3 + CloudFront**: Upload `build/` contents to S3 bucket
- **Any web server**: Serve the `build/` directory contents

## Customization

### Adding New Tools

Edit [data.yml](data.yml) and add items under the appropriate category:

```yaml
categories:
  - name: DDI-CDI Tools
    subcategories:
      - name: DDI-CDI Tools
        items:
          - name: Your Tool Name
            description: Tool description
            homepage_url: https://example.com
            logo: your-logo.png
            project: sandbox  # or incubating, graduated, standard
            joined: "2025-11-12"
            repo_url: https://github.com/user/repo
            license: "MIT License"
```

### Updating Colors & Branding

Edit [settings.yml](settings.yml) to customize:

- Colors (7 color scheme variables)
- Header and footer logos
- Social media links
- Foundation name and description

### Adding Logos

1. Add logo files (PNG/SVG) to the `logos/` directory
2. Reference them in `data.yml` using just the filename
3. SVG format is recommended for best quality

## Documentation

For detailed configuration options, see the landscape2 documentation:

- [Data configuration](https://github.com/cncf/landscape2/blob/main/docs/config/data.yml)
- [Settings configuration](https://github.com/cncf/landscape2/blob/main/docs/config/settings.yml)
- [Guide configuration](https://github.com/cncf/landscape2/blob/main/docs/config/guide.yml)

## About DDI-CDI

The Data Documentation Initiative - Cross Domain Integration (DDI-CDI) is a metadata specification that enables the documentation and exchange of data across different domains and statistical organizations. It provides a standardized framework for representing complex data structures, metadata, and provenance information.

## Contributing

To contribute to this landscape:

1. Fork the repository
2. Add or update entries in [data.yml](data.yml)
3. Add logo files to the [logos/](logos/) directory
4. Test locally using `landscape2 build` and `landscape2 serve`
5. Submit a pull request

## License

The configuration files in this repository are available under the [LICENSE] terms.

Individual tools and projects listed in the landscape maintain their own licenses as specified in their respective entries.

## Links

- DDI Alliance: https://ddialliance.org/
- DDI-CDI Specification: https://ddialliance.org/Specification/DDI-CDI/
- Landscape2 Tool: https://github.com/cncf/landscape2
