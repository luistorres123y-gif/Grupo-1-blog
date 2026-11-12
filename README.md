# RollingCode Blog

A collaborative blog-style web project built to showcase articles, learning paths, and ecosystem updates for the RollingCode community. The project focuses on a modern, responsive front-end experience using HTML, CSS, and Bootstrap, with multiple static pages for navigation, categories, posts, events, and contact.

## Project Overview

This repository contains a fully static blog website designed for educational purposes and content publishing. It includes a homepage with featured posts, category pages, article pages, a contact section, gallery, login UI, and a subscription modal. The project is intended to demonstrate how to structure a blog-like website with reusable sections and a clean, modern visual design.

The application is built as a front-end-only project, with no backend or database integration required for local viewing. It is ideal for learning layout composition, semantic HTML structure, responsive design, and component styling with Bootstrap.

## Key Features

- Responsive homepage with hero carousel and featured content
- Post cards and article listing layout
- Category pages for different topics and tags
- Dedicated pages for About, Contact, Gallery, and Login
- Subscription modal and call-to-action sections
- Clean Bootstrap-based UI with custom CSS styling
- Structured assets folder for media, icons, and other visual resources
- Accessible markup and navigation patterns

## Tech Stack

- HTML5
- CSS3
- Bootstrap 5.3
- Bootstrap Icons
- Google Fonts (Outfit)

## Project Structure

```text
Grupo-1-blog/
├── index.html                 # Homepage
├── about.html                 # About page
├── contact.html               # Contact page
├── gallery.html               # Gallery page
├── login.html                 # Login page
├── 404.html                   # Not found page
├── style.css                  # Global styles
├── CONTRIBUTING.md            # Team workflow and collaboration rules
├── README.md                 # Project documentation
├── assets/                   # Images, icons, and static media
│   ├── img/
│   ├── icons/
│   └── ...
├── pages/                    # Section-specific CSS and component styles
│   ├── navbar/
│   ├── posts/
│   ├── sidebar/
│   ├── cta/
│   ├── footer/
│   ├── chatbot/
│   └── ...
├── categoria-primeros-pasos.html
├── categoria-front-end.html
├── categoria-back-end.html
├── categoria-herramientas.html
├── categoria-eventos.html
├── post-getting-started.html
├── post-semantic-html.html
├── post-bootstrap-grid.html
├── post-git-github.html
├── post-api.html
├── post-portfolio.html
├── post-workshop-ia.html
└── ...
```

## Content and Pages

### Homepage
The homepage serves as the main landing page and contains:

- a hero carousel highlighting key messages
- featured article cards
- educational categories
- call-to-action banners
- stats and ecosystem sections
- recent press mentions and news blocks

### Category Pages
The project includes category pages such as:

- First steps
- Front-end
- Back-end
- Tools
- Events

These pages help organize content and make navigation easier for readers.

### Article Pages
Each article is treated as a standalone content page with a consistent layout. Articles cover topics such as:

- how to start programming
- semantic HTML
- Bootstrap grid system
- Git and GitHub workflow
- APIs
- career portfolio development
- AI and software development trends

### Informational Pages
Additional pages provide project context and user flows, including:

- About us
- Contact
- Gallery
- Login

## Design Overview

The interface uses a dark theme with accent colors and modern typography to create a visually engaging reading experience. The layout is designed around:

- a sticky navigation bar
- spaced card-based content sections
- image-driven articles
- bold section headings
- responsive grids for desktop and mobile screens
- strong visual hierarchy for readability

## Local Setup

No build tools or package installation are required because the site is static.

### Option 1: Open directly in a browser

1. Clone the repository:

```bash
git clone https://github.com/luistorres123y-gif/Grupo-1-blog.git
cd Grupo-1-blog
```

2. Open `index.html` in your browser.

### Option 2: Use a local preview extension

You can also run the project using a VS Code extension such as:

- Live Server

This provides quick reload support while editing files.

## Running the Project

Because the project is static, no special commands are needed to start it. The main entry point is:

```text
index.html
```

Open this file in the browser or serve the folder locally with an HTTP preview tool.

## Styling Philosophy

The project uses a combination of:

- Bootstrap utility classes for layout and responsiveness
- custom CSS for branding, spacing, typography, and section-specific design
- modular organization to keep styles easier to maintain

This structure is suitable for learning how to build a polished, multi-page front-end experience without a framework.

## Collaboration and Workflow

This project follows a structured team workflow defined in [`CONTRIBUTING.md`](CONTRIBUTING.md). It includes conventions for:

- branch naming
- commit messages
- pull request structure
- coding standards
- Git-based collaboration practices

## Contributing

Contributions are welcome. Before starting changes, please review the contribution guidelines to ensure consistency with the repository standards.

## License

This project does not currently specify a license file in the repository.

## Notes

This is a front-end demonstration and educational blog template rather than a production application with user authentication or data persistence. It is designed to showcase UI design, content organization, and responsive web development practices.

## Summary

RollingCode Blog is a static educational blog website created to communicate technology content, learning resources, and community news in a polished and approachable presentation. It demonstrates how to build a responsive, multi-page web experience with HTML, CSS, and Bootstrap while keeping the structure easy to extend and maintain.
