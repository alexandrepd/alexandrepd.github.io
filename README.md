# Alexandre Oliveira | Terminal portfolio

Personal portfolio for a Senior Software Engineer based in Portugal, with a terminal-inspired identity and a focus on .NET/C#, legacy modernization, web and mobile development.

Live: https://alexandrepd.github.io/

## Structure

- `index.html`: HTML, CSS and JavaScript in one file.
- `README.md`: project documentation.

No framework, package installation or build step is required. Google Fonts supplies JetBrains Mono and VT323; system monospace fonts are the fallback.

## Content

- Introduction and selected experience, including 1,050 banking transactions converted to .NET 8 in the BPI modernization program.
- Categorized technical skills, including SQL Server, MySQL, Oracle and InterBase.
- Career timeline, education, certifications, additional training and volunteering.
- Direct links for professional contact and Eureka Genius consulting.
- Optional interactive terminal with command history.

The visible content and terminal responses should be updated together when experience, dates, metrics, technologies or contacts change. The transaction count represents conversions, not certification or production deployment.

## Visual identity and accessibility

- Monospace typography, green accents, ASCII art and subtle CRT texture.
- Low-opacity Matrix background, throttled to approximately 15 frames per second.
- The navigation button and `matrix` command control the same animation state.
- Animation pauses while the tab is hidden.
- `prefers-reduced-motion` disables the Matrix animation and its toggle; changes to the preference are respected while the page is open.
- Static heading and tagline: no glitch, flicker, looping typewriter or full-screen flashes.
- Section navigation, skip link, visible keyboard focus and responsive grids.
- Contact and career information remain available without JavaScript or terminal interaction.
- Native anchor links and browser scroll restoration are preserved.

## Terminal

Available commands:

```text
help · about · skills · experience · education · languages
contact · social · repos · whoami · date · echo <text>
ls · cat <command> · matrix · sudo · clear · exit
```

- Enter executes a command.
- Up/down arrows navigate command history.
- Ctrl+L clears output.
- Output is bounded by a scrollable terminal panel.
- User input and command output are escaped before rendering.
- Commands are limited to the shell's own command dictionary.

This is a portfolio interface, not a system shell. `repos` provides links to the public repository list rather than claiming a fixed set of pinned projects.

## Local preview

Open [index.html](./index.html) directly in a browser. A static server is optional.

## Validation

Before publishing:

1. Run `git diff --check`.
2. Check desktop and narrow mobile widths for overflow and legibility.
3. Test section links and expandable career/training sections.
4. Test terminal commands, unknown commands, history and clear.
5. Test the Matrix button and command, including reduced-motion preferences.
6. Confirm there are no Twitter/X references or outdated dates and metrics.
7. Check direct contact links, page metadata and browser errors.

## Deployment

The repository is a GitHub Pages user site at https://alexandrepd.github.io/.
Publish through the repository's configured Pages deployment after reviewing the changes.

## Credits

- [JetBrains Mono](https://www.jetbrains.com/lp/mono/)
- [VT323](https://fonts.google.com/specimen/VT323)
- Terminal interfaces and classic Matrix code rain.
