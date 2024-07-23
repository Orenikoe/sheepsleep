## Table of Contents
- [Prerequisites](#prerequisites)
- [Project Setup](#project-setup)
- [Project Structure](#project-structure)
- [Scripts](#scripts)
- [Environment Variables](#environment-variables)
- [Deployment](#deployment)
- [Testing](#testing)
- [Advanced Configuration](#advanced-configuration)
- [Troubleshooting](#troubleshooting)
- [Contributing](#contributing)
- [License](#license)
- [Contact Information](#contact-information)
- [Acknowledgments](#acknowledgments)
## Installation

1. **Clone the repository:**
    ```sh
    git clone https://github.com/emma-sleep/wholesale-storefront.git
    cd wholesale-storefront
    ```

2. **Install dependencies:**
    ```sh
    yarn install
    ```

### Running the Development Server

3. **Start the development server:**
    ```sh
    yarn dev
    ```

4. **Open your browser and visit:**
    ```
    http://localhost:3000
    ```

### Additional Scripts

Here are some additional scripts you might find useful:

- **Build the project:**
    ```sh
    yarn build
    ```

- **Start the production server:**
    ```sh
    yarn start
    ```

- **Run tests:**
    ```sh
    yarn test
    ```

- **Run Storybook:**
    ```sh
    yarn storybook
    ```

- **Build Storybook:**
    ```sh
    yarn build-storybook
    ```

- **Lint the code:**
    ```sh
    yarn lint
    ```

### Environment Variables

The project uses environment variables for configuration. You can set them in a `.env.local` file in the root of the project. Here are some common variables:

- `APP_ENV` - Set the application environment (e.g., `dev`, `prod`).
- `NEXT_PUBLIC_API_MOCKING` - Enable or disable API mocking.
- `NEXT_PUBLIC_IS_ADMIN` - Enable or disable admin mode.

### Project Structure

```plaintext
├── public/               # Public assets like images, fonts, etc.
├── src/                  # Source files
│   ├── components/       # React components
│   ├── hooks/            # Custom hooks
│   ├── pages/            # Next.js pages
│   ├── styles/           # CSS and SCSS files
│   ├── utils/            # Utility functions
│   ├── locales/          # Localization files
├── .env.local            # Environment variables
├── package.json          # Package configuration
├── yarn.lock             # Yarn lock file
└── README.md             # Project documentation
