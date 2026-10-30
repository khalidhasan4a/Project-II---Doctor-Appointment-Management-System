# Doctor Finder – Doctor Appointment Management System

A browser-based doctor discovery and appointment booking project for **Tangail Zila Sadar Hospital & Clinic**. The application lets visitors find doctors, review available appointment dates, submit patient details, and view or print an appointment slip. It also includes an administrative interface for managing appointment status.

> **Project status:** Academic project / prototype. Review the security and deployment notes before using it with real patient information or publishing it for public use.

## Features

### For patients and visitors

- Find doctors using hospital, department, speciality, and doctor-name filters.
- View doctor information and open the appointment booking form.
- Select a doctor and an available appointment date.
- View daily slot availability. The interface is configured with a limit of 15 appointments per doctor per day.
- Book as a new patient or an existing patient.
- Enter patient details and identification information (NID, Birth Registration, Tika Card, or Passport).
- Receive an appointment/registration number in the booking confirmation screen.
- Download or print the appointment slip as a PDF.
- Check appointment information using a registration number or mobile number.

### For administrators

The project includes an administrative interface with features for appointment administration, including:

- Admin sign-in and password-reset interface.
- Review and confirm or cancel appointments.
- View appointment status and patient/booking information.
- Export appointment information to an Excel file.
- Use the available backup interface.

The actual authentication and data-storage approach should be reviewed before real-world deployment; see [Security and privacy](#security-and-privacy).

### Email notification (optional integration)

The project contains an optional email module intended to send appointment notifications through a Google Apps Script web app. The email template can include appointment details, and the generated appointment slip can be attached as a PDF.

Email delivery depends on a correctly authorized and deployed Apps Script endpoint. Configure and test this integration separately; do not assume that email delivery is active simply because an appointment was booked. The current project setup has required further testing of deployment access and request handling.

## Technology

- HTML5
- CSS3
- Vanilla JavaScript
- [SheetJS](https://cdnjs.cloudflare.com/ajax/libs/xlsx/0.18.5/xlsx.full.min.js) for Excel export
- [jsPDF](https://cdnjs.cloudflare.com/ajax/libs/jspdf/2.5.1/jspdf.umd.min.js) for PDF generation
- Google Apps Script and Gmail for the optional email integration

The SheetJS and jsPDF libraries are loaded from CDN links in `index.html`, so an internet connection is required for those features unless the libraries are hosted locally.

## Project structure

```text
Doctor-Finder/
├── index.html
├── css/
│   └── style.css
├── js/
│   ├── data.js
│   ├── geo.js
│   ├── utils.js
│   ├── storage.js
│   ├── dropdown.js
│   ├── finder.js
│   ├── slip.js
│   ├── mailer.js
│   ├── booking.js
│   ├── appointments.js
│   ├── admin.js
│   ├── status.js
│   └── main.js
├── email-setup/
│   └── SETUP.md                # Keep private deployment details out of a public repo
├── .gitignore
└── README.md
```

The exact files in your local project may differ as development continues. Do not commit private Apps Script source, credentials, patient records, database files, backups, or deployment secrets to a public repository.

## Run locally

This is a static front-end project. You can run it locally with Visual Studio Code and the Live Server extension.

1. Clone or download the repository.
2. Open the project folder in Visual Studio Code.
3. Install the **Live Server** extension if it is not already installed.
4. Open `index.html` and select **Open with Live Server**.
5. The site should open in your browser, usually at an address such as `http://127.0.0.1:5500/`.

You can also serve the folder with another local static web server. Avoid relying on `file://` URLs because local scripts and browser features may behave differently.

## Appointment workflow

1. A visitor searches for a doctor and opens the booking form.
2. The visitor selects a speciality/doctor and an available date.
3. The visitor enters the required patient details and submits the appointment.
4. The site displays the appointment number, registration number, serial number, and slip actions.
5. An administrator can review the appointment and update its status through the admin interface.
6. The visitor can use **Check Appointment** to look up the appointment with the registration number or mobile number.

## Optional email setup

The email integration uses a Google Apps Script web app that sends email from the Google account that owns and authorizes the script.

Before enabling it:

1. Create the Apps Script project while signed in to the intended sender account.
2. Add the server-side email code and authorize the required Gmail sending permission.
3. Deploy it as a web app with an access policy that permits the intended website visitors to call it.
4. Configure the web app URL in `js/mailer.js`.
5. Test with an address you control and confirm both the email body and PDF attachment.

**Important:** A secret placed in `js/mailer.js` is visible to anyone who can load the website. A front-end token is not a secure authentication mechanism. For a public deployment, move email sending to a trusted server/backend, protect the endpoint, validate requests, and apply rate limiting or abuse prevention. Do not publish a live Apps Script secret or private deployment configuration.

## Security and privacy

This project collects sensitive personal information, including identity-document details, contact information, and patient details. Treat it as sensitive data.

- Do not commit real patient data, populated backups, credentials, API keys, tokens, or `.env` files.
- Keep the GitHub repository private while removing secrets and reviewing the code. Making a repository private does not remove secrets from its commit history or make client-side secrets safe.
- Do not use this prototype for real patient records until data storage, access control, administrator authentication, transport security, backups, retention, and privacy requirements have been reviewed and implemented appropriately.
- Do not rely on browser-side checks or front-end JavaScript for authorization or protection of patient records.
- If a token or password has been exposed, rotate it. Removing it from the latest file alone does not erase it from earlier Git commits.

## Contributors

- **Md. Khalid Hasan** — IT24013
- **Alif Ahmed Joy** — IT24015

## License

No open-source license has been specified yet. Unless a license is added, all rights remain with the copyright holder(s), and others do not automatically receive permission to reuse or distribute the code.
