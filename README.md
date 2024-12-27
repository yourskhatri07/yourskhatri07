import requests
from bs4 import BeautifulSoup

def check_instagram_user(username):
    url = f"https://www.instagram.com/{username}/"
    headers = {
        'User-Agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.3'}

    response = requests.get(url, headers=headers)

    if response.status_code == 200:
        soup = BeautifulSoup(response.content, 'html.parser')
        if soup.find('meta', property='og:title') and 'Instagram' in soup.find('meta', property='og:title').get('content', ''):
            print(f"Username {username} exists on Instagram.")
        else:
            print(f"Username {username} does not exist on Instagram.")
    else:
        print(f"Error: Unable to access the URL. Status code:
