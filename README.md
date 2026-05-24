# 📰 AajTak News API - Free & Always Updated

> **Free Hindi News API** — Aaj Tak ki latest news, har ghante auto-update hoti hai.  
> Koi server nahi, koi cost nahi, koi rate limit nahi! 🚀

---

## ⚡ API Endpoints

Base URL: `https://raw.githubusercontent.com/sunketbot/NewsData/main/`

| Category | Endpoint URL |
|---|---|
| 🏠 Latest News | `https://raw.githubusercontent.com/sunketbot/NewsData/main/latest.json` |
| 🏛️ Politics | `https://raw.githubusercontent.com/sunketbot/NewsData/main/politics.json` |
| 💻 Technology | `https://raw.githubusercontent.com/sunketbot/NewsData/main/tech.json` |
| 💼 Business | `https://raw.githubusercontent.com/sunketbot/NewsData/main/business.json` |
| 📈 Stock Market | `https://raw.githubusercontent.com/sunketbot/NewsData/main/stock.json` |
| 🍕 Food | `https://raw.githubusercontent.com/sunketbot/NewsData/main/food.json` |
| 🏏 Sports | `https://raw.githubusercontent.com/sunketbot/NewsData/main/sports.json` |
| 🎬 Entertainment | `https://raw.githubusercontent.com/sunketbot/NewsData/main/entertainment.json` |
| 🌍 World | `https://raw.githubusercontent.com/sunketbot/NewsData/main/world.json` |
| 🔍 Search Index (All News) | `https://raw.githubusercontent.com/sunketbot/NewsData/main/search.json` |
| 📋 All Endpoints List | `https://raw.githubusercontent.com/sunketbot/NewsData/main/index.json` |

---

## 📦 Response Format

```json
{
  "status": "success",
  "category": "tech",
  "count": 10,
  "last_updated": "2026-05-24T17:00:00+05:30",
  "data": [
    {
      "id": "abc123",
      "url": "https://www.aajtak.in/...",
      "source": "Aaj Tak",
      "title": "News ka title",
      "description": "Poori news ka 2-3 sentence ka summary",
      "image": "https://...jpg",
      "published_date": "2026-05-24T16:55:00+05:30",
      "modified_date": "2026-05-24T16:55:00+05:30",
      "keywords": "keyword1, keyword2",
      "category": "tech"
    }
  ]
}
```

---

## 🔍 Search Feature

`search.json` mein **saari categories ki news** ek jagah hoti hai — **latest first**.  
Aap local search implement kar sakte ho:

```javascript
// JavaScript / React Native
async function searchNews(query) {
    const res = await fetch(
        'https://raw.githubusercontent.com/sunketbot/NewsData/main/search.json'
    );
    const data = await res.json();
    
    // Filter by title, description ya keywords
    return data.data.filter(news =>
        news.title.toLowerCase().includes(query.toLowerCase()) ||
        news.description.toLowerCase().includes(query.toLowerCase()) ||
        news.keywords.toLowerCase().includes(query.toLowerCase())
    );
    // Already sorted: latest first ✅
}
```

---

## 📱 Usage Examples

### JavaScript (Fetch)
```javascript
// Tech news fetch karo
fetch('https://raw.githubusercontent.com/sunketbot/NewsData/main/tech.json')
  .then(res => res.json())
  .then(data => {
    data.data.forEach(news => {
      console.log(news.title);    // News title
      console.log(news.image);    // Thumbnail image URL
      console.log(news.description); // Full news summary
      console.log(news.published_date); // Date (latest first)
    });
  });
```

### Python
```python
import requests

# Latest news fetch karo
r = requests.get('https://raw.githubusercontent.com/sunketbot/NewsData/main/latest.json')
data = r.json()

for news in data['data']:
    print(f"Title: {news['title']}")
    print(f"Date:  {news['published_date']}")
    print(f"Image: {news['image']}")
    print(f"Link:  {news['url']}")
    print("---")
```

### PHP
```php
<?php
$response = file_get_contents('https://raw.githubusercontent.com/sunketbot/NewsData/main/politics.json');
$data = json_decode($response, true);

foreach ($data['data'] as $news) {
    echo $news['title'] . "\n";
    echo $news['image'] . "\n";
    echo $news['published_date'] . "\n";
}
```

### Dart (Flutter)
```dart
import 'dart:convert';
import 'package:http/http.dart' as http;

Future<List> fetchNews(String category) async {
  final res = await http.get(Uri.parse(
    'https://raw.githubusercontent.com/sunketbot/NewsData/main/$category.json'
  ));
  final data = jsonDecode(res.body);
  return data['data']; // Latest first!
}
```

---

## ⏱️ Update Frequency

- **Auto-update:** Har 1 ghante mein (GitHub Actions se)
- **Manual update:** Repo owner kabhi bhi trigger kar sakta hai
- `last_updated` field mein exact time hota hai jab news last fetch hui

---

## 🔄 News Sorting

Saari news **latest (newest) se purani** sort hoti hai:
- `data[0]` = sabse nayi khabar
- `data[last]` = sabse purani khabar

---

## ⚠️ Important Notes

- Yeh API **read-only** hai — sirf GET requests support hoti hain
- Data source: **Aaj Tak** (www.aajtak.in)
- Language: **Hindi**
- Koi authentication nahi chahiye
- Koi rate limit nahi hai (GitHub CDN se serve hota hai)

---

## 🛠️ Powered By

- **GitHub Actions** — Automation
- **GitHub Raw CDN** — Free, Fast Hosting
- **Aaj Tak** — News Source
