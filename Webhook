# Python example using Flask for simplicity, but you can use any web framework

from flask import Flask, request
import requests

app = Flask(__name__)

TELEGRAM_TOKEN = "7127091359:AAHow20sVOE3GWe05TXgiIwk0Mp7iUYY77k"
GITHUB_TOKEN = "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"

@app.route('/webhook', methods=['POST'])
def webhook():
    update = request.json
    chat_id = update['message']['chat']['id']
    text = update['message']['text']
    
    # Process incoming message
    if text == '/latest_issue':
        latest_issue = get_latest_issue()
        send_message(chat_id, latest_issue)
    
    return 'OK'

def get_latest_issue():
    # Use GitHub API to fetch the latest issue from your repository
    url = 'https://github.com/ghosthash2/Degen-Bets-4.git'
    headers = {'Authorization': f'token {GITHUB_TOKEN}'}
    response = requests.get(url, headers=headers)
    latest_issue = response.json()[0]['title']
    return latest_issue

def send_message(chat_id, text):
    # Send message to Telegram
    url = f'https://api.telegram.org/bot{TELEGRAM_TOKEN}/sendMessage'
    payload = {'chat_id': chat_id, 'text': text}
    requests.post(url, json=payload)

if __name__ == '__main__':
    app.run()
