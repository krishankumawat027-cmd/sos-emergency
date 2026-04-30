# Emergency SOS Web App

Emergency SOS is a Flask-based web app that helps a user send an SOS alert to saved emergency contacts. The app captures the user's live location in the browser and sends an SMS alert through Fast2SMS.

## Features

- Add and store emergency contacts in `contacts.json`
- Capture live location from the browser
- Send SOS SMS alerts with a Google Maps link
- Voice-trigger support in the frontend UI
- Camera preview and local image capture in the browser
- Simple Render deployment config included

## Project Structure

```text
app.py
requirements.txt
render.yaml
contacts.json
templates/
static/
```

## Requirements

- Python 3.10+ recommended
- A Fast2SMS API key

## Environment Variables

Create a `.env` file in the project root:

```env
FAST2SMS_API_KEY=your_fast2sms_api_key
FLASK_DEBUG=true
PORT=5000
```

## Install

```powershell
py -m pip install -r requirements.txt
```

If `py` does not work, use:

```powershell
python -m pip install -r requirements.txt
```

## Run Locally

```powershell
py app.py
```

Then open:

```text
http://127.0.0.1:5000/dashboard
```

## Main Routes

- `GET /` : backend health response
- `GET /dashboard` : main frontend dashboard
- `POST /add-contact` : save a contact
- `GET /contacts` : fetch saved contacts
- `GET /test-sms` : send a test SMS
- `POST /send-sos` : send SOS SMS to all saved contacts

## Contacts Storage

Contacts are stored in:

```text
contacts.json
```

Phone numbers may be stored as `+91...` or `10-digit`, and the backend normalizes them before sending SMS.

## Deployment

This project already includes `render.yaml` for Render.

### Render Steps

1. Push the project to GitHub.
2. Create a new Render Web Service.
3. Connect your GitHub repository.
4. Add environment variable:
   `FAST2SMS_API_KEY=your_fast2sms_api_key`
5. Deploy.

Render uses:

```text
Build: pip install -r requirements.txt
Start: gunicorn app:app
```

## Notes

- The app depends on browser permissions for location, microphone, and camera.
- SMS delivery depends on Fast2SMS API availability and account status.
- `contacts.json` is local file storage, so it is not suitable for multi-user production use.

## Future Improvements

- Store SOS logs in the backend
- Add contact delete and edit options
- Use a database instead of JSON storage
- Add authentication for dashboard access
- Add proper production logging
