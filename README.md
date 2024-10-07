# EC601-Project2
# Product mission statement:
# To translate food name on the menu accurately for international student from China.
# Product user stories:
# As an international student from China, the biggest problem I have encountered is that I cannot understand the menu in restaurant. Thus, to improve the experience in ordering food, I’d like to develop a food translation product. 
# MVP:
# Receiving English food name and translate into Chinese name.
# APIS:
# Google Translate API
import requests


def translate_text(text, target_language="zh", api_key="YOUR_API_KEY"):
    url = "https://translation.googleapis.com/language/translate/v2"
    params = {
        'q': text,
        'target': target_language,
        'key': api_key
    }

    response = requests.get(url, params=params)

    if response.status_code == 200:
        result = response.json()
        return result['data']['translations'][0]['translatedText']
    else:
        raise Exception(f"Error: {response.status_code}, {response.text}")


if __name__ == "__main__":
    api_key = "AIzaSyCRg4cP6vRDcQcpS_0WbxgD2urDwgHMoUE"

    while True:
        dish = input("请输入要翻译的英文菜名（输入'q'退出）：")
        if dish.lower() == 'q':  
            print("程序已退出。")
            break
        translated_dish = translate_text(dish, api_key=api_key)
        print(f"英文菜名: {dish} -> 中文翻译: {translated_dish}")
