# ResuMate – AI Resume Analyzer

ResuMate is an AI-powered resume analysis tool built with React, TypeScript, Tailwind CSS, Vite, and Zustand, and powered by the Puter.js AI APIs.

It helps job applicants improve their resumes by providing ATS scores, personalized feedback, and job-resume matching reports.

---

## 🚀 Features

-   📄 **Resume Upload & Validation**: Upload PDF resumes (max 20MB) with client-side validation.
-   🖼️ **PDF-to-Image Conversion**: Converts resume PDFs into images for AI processing.
-   🤖 **AI Resume Analysis**: Generates an in-depth analysis including:
    -   ATS Score
    -   Contextual feedback
    -   Job-role specific impressions
    -   Suggested improvements
-   🔗 **Job Context Integration**: Accepts inputs like Job Description, Role, and Company Name to tailor the analysis.
-   ☁️ **Cloud-Powered Backend (via Puter.js)**: Handles authentication, file storage, AI feedback, and metadata storage.
-   🎨 **Modern UI**: A fully responsive, mobile-friendly design built with Tailwind CSS.
-   ⚡ **Client-Side Only**: The entire application runs in the browser, with all backend services handled by the Puter.js SDK, requiring no custom server.

## 🛠️ Tech Stack

-   **Frontend**: React, TypeScript, Vite
-   **Styling**: Tailwind CSS
-   **State Management**: Zustand
-   **External API**: Puter.js (for Auth, File Storage, AI, and KV Store)

## 🧩 System Architecture

ResuMate follows a React Router v7-based architecture with four main routes:

| Route          | File Path             | Purpose                                |
| :------------- | :-------------------- | :------------------------------------- |
| `/`            | `/routes/home.tsx`    | Landing page & dashboard               |
| `/auth`        | `/routes/auth.tsx`    | Authentication flow                    |
| `/upload`      | `/routes/upload.tsx`  | Resume upload & analysis pipeline      |
| `/resume/:id`  | `/routes/resume.tsx`  | Results display page                   |

## 🔄 Analysis Pipeline

The resume analysis process follows these steps:

1.  **File Upload**: The resume PDF is uploaded to Puter file storage using `fs.upload`.
2.  **Image Conversion**: The uploaded PDF is converted to an image using a client-side library.
3.  **Image Upload**: The converted image is then stored in Puter storage.
4.  **Data Preparation**: Metadata (job title, description, etc.) is saved with a unique UUID via `kv.set`.
5.  **AI Analysis**: AI feedback is generated using `ai.feedback` with a custom-engineered prompt.
6.  **Result Storage**: The final analysis results are saved and displayed to the user.

### Data Object Example

Here is an example of the data structure used to store analysis metadata:

```json
{
  "id": "a1b2c3d4-e5f6-7890-1234-567890abcdef",
  "resumePath": "/resumes/user123/my_resume.pdf",
  "imagePath": "/images/user123/my_resume.png",
  "companyName": "Tech Solutions Inc.",
  "jobTitle": "Frontend Developer",
  "jobDescription": "Looking for a skilled React developer...",
  "feedback": {
    "atsScore": 85,
    "impressions": "The resume strongly aligns with frontend technologies...",
    "improvements": "Consider adding quantitative metrics to your project descriptions..."
  }
}
```

## 📦 Core Services via Puter.js

The application leverages the following services from the Puter.js SDK:

| Service      | Key Functions                          | Purpose                               |
| :----------- | :------------------------------------- | :------------------------------------ |
| **Auth** | `signIn()`, `signOut()`, `checkAuth()` | User authentication and session management. |
| **File System**| `upload()`, `write()`, `read()`, `delete()` | Resume & image storage in the cloud.  |
| **AI** | `chat()`, `feedback()`, `img2txt()`    | Resume analysis & feedback generation. |
| **KV Store** | `get()`, `set()`, `list()`, `delete()` | Metadata and result storage.          |

## ⚡ Getting Started

Follow these steps to get the project running locally.

**1. Clone the repository**

```bash
git clone [https://github.com/your-username/resumate.git](https://github.com/your-username/resumate.git)
cd resumate
```

**2. Install dependencies**

```bash
npm install
```

**3. Start the development server**

```bash
npm run dev
```

**4. Build for production**

```bash
npm run build
```

## 📌 Future Improvements

-   Add support for optional local analysis to expand beyond Puter.js.
-   Add support for `DOCX` and other common resume formats.
-   Improve the visualization of results with charts and graphs.
-   Implement multi-language resume analysis capabilities.
