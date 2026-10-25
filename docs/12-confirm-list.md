# Developer Verification List [CONFIRM WITH DEVELOPER]

1. **Rebranding Context**: Confirm whether the rebrand from "Natours" to "Wanderly" in `01_Natours/README.md` was undertaken for a specific portfolio submission or client demo.
2. **Icon Font Source**: Verify if the Linea basic icon font in `css/fonts/` can be migrated to inline SVGs to eliminate binary font loading latency.
3. **Target Browser Support**: Confirm whether IE11 compatibility is still required, or if the PostCSS Autoprefixer target can be modernized to `> 0.5%, last 2 versions, not dead`.
4. **Form Submission Target**: Confirm whether the booking form in `index.html` is intended to connect to a serverless AWS Lambda function or a Node.js REST API.
