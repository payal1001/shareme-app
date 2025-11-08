# ShareMe - Full-Stack Image Sharing Platform

ShareMe is a full-stack social media application inspired by Pinterest. It allows users to discover, save, and share image-based "pins" with the community. The application features a modern, responsive user interface and is powered by a headless CMS for content management.

![ShareMe Screenshot](https://i.ibb.co/G5g46w2/image.png)

## Features

*   **Google Authentication:** Secure and easy sign-in/sign-up using Google OAuth.
*   **Create & Manage Pins:** Users can upload images, add titles, descriptions, and destination links to create new pins.
*   **Discover Pins:** A masonry-layout feed to browse pins from all users.
*   **Pin Details:** View detailed information about a specific pin, including comments and related posts.
*   **Search Functionality:** Find pins based on categories or keywords.
*   **User Profiles:** View user-specific profiles with all their created and saved pins.
*   **Content Management:** A separate Sanity Studio to manage users, pins, and comments directly.
*   **Responsive Design:** A seamless experience across desktop, tablet, and mobile devices.

## Tech Stack

The project is divided into two main parts: a React-based frontend and a Sanity.io backend.

### Frontend (`shareme_frontend-main`)

*   **Framework:** React.js
*   **Styling:** Tailwind CSS
*   **Routing:** React Router
*   **State Management:** React Hooks (useState, useEffect)
*   **Authentication:** @react-oauth/google
*   **API Client:** @sanity/client
*   **Image Handling:** @sanity/image-url
*   **Layout:** React Masonry CSS

### Backend (`Shareme_backend-main`)

*   **CMS:** Sanity.io
*   **Schema:** Custom schemas for `user`, `pin`, `comment`, etc.
*   **Plugins:** Desk Tool, Vision

## Getting Started

Follow these instructions to get a local copy of the project up and running.

### Prerequisites

*   Node.js (v14 or later)
*   npm or yarn

### 1. Backend Setup (Sanity Studio)

The backend is a Sanity Content Studio that you will run locally to manage your data.

1.  **Navigate to the backend directory:**
    ```bash
    cd Shareme_backend-main
    ```

2.  **Install dependencies:**
    ```bash
    npm install
    ```

3.  **Configure Sanity Project:**
    You will need to create your own Sanity project to connect the studio.
    *   Visit sanity.io/manage to create a new project.
    *   Update `Shareme_backend-main/sanity.config.js` with your new `projectId` and `dataset`:
        ```javascript
        // sanity.config.js
        export default defineConfig({
          // ...
          projectId: 'YOUR_PROJECT_ID',
          dataset: 'production',
          // ...
        })
        ```

4.  **Run the Sanity Studio:**
    ```bash
    npm run dev
    ```
    The studio will be available at `http://localhost:3333`. You can use it to define your content schemas and manage data.

### 2. Frontend Setup (React App)

1.  **Navigate to the frontend directory:**
    ```bash
    cd shareme_frontend-main
    ```

2.  **Install dependencies:**
    ```bash
    npm install
    ```

3.  **Create Environment Variables:**
    Create a `.env` file in the `shareme_frontend-main` root directory and add the following variables. Replace the placeholder values with your own from Google Cloud Console and your Sanity project.

    ```env
    REACT_APP_GOOGLE_API_TOKEN=YOUR_GOOGLE_CLIENT_ID
    REACT_APP_SANITY_PROJECT_ID=YOUR_SANITY_PROJECT_ID
    ```

4.  **Run the React application:**
    ```bash
    npm start
    ```
    The application will open at `http://localhost:3000`.

## Project Structure

```
shareme/
├── README.md                # Main project README
├── Shareme_backend-main/    # Sanity.io backend and content studio
│   ├── schemas/             # Content model schemas (user, pin, etc.)
│   └── sanity.config.js     # Sanity project configuration
└── shareme_frontend-main/   # React frontend application
    ├── public/
    └── src/
        ├── assets/
        ├── components/      # Reusable React components
        ├── container/
        └── client.js        # Sanity client configuration
```

## Data Models

The content models for the application are defined as schemas in the Sanity backend. The primary models are `user`, `pin`, and `comment`.

### `pin` Schema

Based on the `CreatePin.jsx` component, the `pin` document has the following structure:

| Field         | Type                               | Description                                     |
| :------------ | :--------------------------------- | :---------------------------------------------- |
| `title`       | `string`                           | The title of the pin.                           |
| `about`       | `string`                           | A short description of the pin.                 |
| `destination` | `url`                              | The destination URL when a user clicks the pin. |
| `category`    | `string`                           | The category the pin belongs to.                |
| `image`       | `image`                            | The main image asset for the pin.               |
| `userId`      | `string`                           | The ID of the user who posted the pin.          |
| `postedBy`    | `reference` -> `user`              | A reference to the `user` document.             |
| `save`        | `array` of `save` objects          | A list of users who have saved the pin.         |
| `comments`    | `array` of `comment` objects       | A list of comments on the pin.                  |

### `user` Schema

| Field      | Type     | Description                           |
| :--------- | :------- | :------------------------------------ |
| `userName` | `string` | The user's display name.              |
| `image`    | `url`    | The URL for the user's profile image. |

### `comment` Schema

| Field      | Type                          | Description                         |
| :--------- | :---------------------------- | :---------------------------------- |
| `postedBy` | `reference` -> `user`         | The user who posted the comment.    |
| `comment`  | `string`                      | The text content of the comment.    |

## Deployment

*(This is a placeholder section. You can add your specific deployment steps here.)*

### Backend
The Sanity Studio can be deployed by running `sanity deploy` from the `Shareme_backend-main` directory. This will deploy the content studio to a `*.sanity.studio` subdomain.

### Frontend
The React frontend can be deployed to any static site hosting service like Netlify, Vercel, or GitHub Pages. A standard build can be created by running `npm run build` in the `shareme_frontend-main` directory.

## Contributing

Contributions are welcome! Please feel free to submit a pull request.

1.  Fork the Project
2.  Create your Feature Branch (`git checkout -b feature/AmazingFeature`)
3.  Commit your Changes (`git commit -m 'Add some AmazingFeature'`)
4.  Push to the Branch (`git push origin feature/AmazingFeature`)
5.  Open a Pull Request

## License

This project is currently unlicensed.
