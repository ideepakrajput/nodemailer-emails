# Bulk Email Application

A robust Node.js application designed for efficient bulk email dispatch using Gmail's OAuth2 authentication. This tool ensures reliable delivery with retry mechanisms and detailed reporting.

## Features

- **Bulk Dispatch**: Seamlessly send emails to multiple recipients.
- **Resilience**: Automatic retry logic (up to 3 attempts) for failed deliveries.
- **Batch Processing**: Optimizes throughput by processing emails in batches.
- **Detailed Reporting**: Generates a comprehensive JSON report (`email_sending_report.json`) of delivery statuses.
- **Secure Authentication**: Utilizes OAuth2 for secure integration with Gmail.
- **Validation**: Includes input validation for email addresses.

## Prerequisites

- **Node.js**: v14.x or higher ([Download](https://nodejs.org/))
- **npm**: Package manager (included with Node.js)
- **Google Account**: A Gmail account for sending emails.
- **Google Cloud Console Project**: With Gmail API enabled.

## Installation & Setup

### 1. Clone the Repository

```bash
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configuration

1.  Create a `.env` file in the project root.
2.  Populate it with your Google API credentials:

    ```env
    G_USER_EMAIL=your-email@gmail.com
    G_CLIENT_ID=your-client-id
    G_CLIENT_SECRET=your-client-secret
    G_REFRESH_TOKEN=your-refresh-token
    G_REDIRECT_URI=https://developers.google.com/oauthplayground
    ```

### 4. Google Cloud Setup

To obtain the necessary Client ID and Client Secret:

1.  Navigate to the [Google Cloud Console](https://console.cloud.google.com/).
2.  Create a new project or select an existing one.
3.  **Enable Gmail API**: Go to "APIs & Services" > "Library", search for "Gmail API", and enable it.
4.  **Create Credentials**:
    -   Go to "APIs & Services" > "Credentials".
    -   Click "Create Credentials" > "OAuth client ID".
    -   Select "Web application" as the application type.
    -   **Configure Authorized Redirect URI**:
        1.  Scroll down to the **Authorized redirect URIs** section.
        2.  Click **Add URI**.
        3.  Paste the exact URL: `https://developers.google.com/oauthplayground`
        4.  *Note: Ensure there are no trailing slashes or spaces.*
        5.  Click **Save**.
5.  Copy the **Client ID** and **Client Secret** and paste them into your `.env` file.

### 5. Generate Refresh Token

If you need to generate or regenerate your Refresh Token, follow these steps:

1.  Open the [OAuth 2.0 Playground](https://developers.google.com/oauthplayground).
2.  Click the **Gear Icon** (Configuration) in the top right corner.
3.  Check the box **"Use your own OAuth credentials"**.
4.  Enter your credentials from the `.env` file:
    -   **OAuth Client ID**: `********************.apps.googleusercontent.com`
    -   **OAuth Client Secret**: `********************`
5.  In the scopes list, find and select `https://mail.google.com/`.
6.  Click **Authorize APIs**.
7.  Click **Exchange authorization code for tokens**.
8.  Copy the new **Refresh Token**.
9.  Update your `.env` file with this new token value.

## Usage

## Usage

1.  **Prepare Raw Email List**: Create a file named `emails.txt` in the root directory. Add your raw email list (one per line or separated by spaces/commas).
2.  **Validate Emails**: Run the validator script to clean, validate, and remove duplicate emails.
    
    ```bash
    node emailValidator.js
    ```
    
    *This will generate a clean `email_list.txt` file.*

3.  **Prepare Attachments**: Place your resume or attachment in the root directory. Ensure the filename matches the one specified in `index.js` (e.g., `DeepakRajput.pdf`).
4.  **Execute Application**:

    ```bash
    npm start
    ```

## Output

After execution, the application generates:

-   `email_sending_report.json`: A log file detailing successful sends and any failures.

## Project Structure

```text
.
├── emails.txt              # Raw input email list
├── email_list.txt          # Cleaned & validated email list
├── [resume_name].pdf       # Attachment file
├── emailValidator.js       # Email validation utility
├── index.js                # Main application entry point
├── .env                    # Environment variables (GitIgnored)
├── .gitignore              # Git ignore rules
└── README.md               # Project documentation
```

## Best Practices

-   **Sending Limits**: Be aware of [Gmail's daily sending limits](https://support.google.com/a/answer/166852?hl=en) to avoid account suspension.
-   **Security**: Never commit your `.env` file to version control.

## License

This project is open-sourced under the [MIT License](https://opensource.org/licenses/MIT).

## Resources

-   [Nodemailer Documentation](https://nodemailer.com/usage/using-gmail/)
-   [Google Cloud Credentials](https://console.cloud.google.com/apis/credentials)