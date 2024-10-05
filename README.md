# SpyFans Platform Integration Guide

This guide explains how to integrate with the SpyFans platform to retrieve trending videos.

## API Endpoint

Send a POST request to:

```
https://app.spyfans.co/api/external/videos
```

## Request Body

The request body should be a JSON object with the following structure:

```json
{
  "integration": "YOUR_PLATFORM_NAME",
  "secret": "YOUR_PLATFORM_SECRET",
  "api_key": "YOUR_CLIENTS_API_KEY",
  "timeDuration": "Past 24h",
  "searchMode": "Trending",
  "platform": "INSTAGRAM",
  "skip": 0,
  "type": "video",
  "niches": [],
  "countries": [],
  "minVideoViews": 0,
  "minFollowersCount": 0,
  "maxFollowersCount": 100000000
}
```

### Parameters

- `integration`: Set this to "YOUR_PLATFORM_NAME".
- `secret`: Use the provided secret key "YOUR_PLATFORM_SECRET".
- `api_key`: Replace "YOUR_CLIENTS_API_KEY" with your actual API key.
- `timeDuration`: Specifies the time range for trending videos. Options are:
  - "Past 24h"
  - "Past Week"
  - "Past Month"
- `searchMode`: Set to either "Trending" or "Most Views".
- `platform`: Specifies the social media platform. Options are:
  - "INSTAGRAM"
  - "TIKTOK"
- `skip`: Number of results to skip (for pagination).
- `type`: Content type to retrieve. Options are:
  - "video"
  - "slide"
- `niches`: An array of niches to filter by. Available options:
  ["white", "big tits", "blond", "teen", "trans", "role playing", "gym", "yoga", "cosplay", "gamer", "anime", "teacher", "student", "nurse", "brunette", "face", "tattos", "big ass", "chubby", "color hair", "latina", "small tits", "thin", "black", "redhead", "milf", "asian", "pregnant", "small ass", "toung"]
- `countries`: An array of country codes to filter by. Available options:
  ["US", "GB", "CO", "CA", "AU", "DE", "MX", "BR", "ES", "AR", "FR", "RO", "IT", "NL", "PL", "DO", "FI", "PH", "IE", "EC", "CL"]
- `minVideoViews`: Minimum number of views for the videos.
- `minFollowersCount`: Minimum number of followers for the content creator.
- `maxFollowersCount`: Maximum number of followers for the content creator.

## Response

The API returns a list of video objects in JSON format. Each video object contains various properties, including `isCDN`.

### Important Note:

Only use videos where `isCDN` is `true`. These videos are stored in our cache for faster access and better performance.

For videos with `isCDN: true`, use the following URL structures:

- Video file: `https://cdn.spyfans.co/videos/{id}.mp4`
- Thumbnail: `https://cdn.spyfans.co/images/{id}.jpg`
- TikTok slide music: `https://cdn.spyfans.co/musics/{id}.mp3`

Replace `{id}` with the actual ID of the video.

## Example Usage

Here's an example of how to make the API request using cURL:

```bash
curl -X POST https://app.spyfans.co/api/external/videos \
     -H "Content-Type: application/json" \
     -d '{
         "integration": "YOUR_PLATFORM_NAME",
         "secret": "YOUR_PLATFORM_SECRET",
         "api_key": "YOUR_CLIENTS_API_KEY",
         "timeDuration": "Past 24h",
         "searchMode": "Trending",
         "platform": "INSTAGRAM",
         "skip": 0,
         "type": "video",
         "niches": ["cosplay", "gamer"],
         "countries": ["US", "CA"],
         "minVideoViews": 1000,
         "minFollowersCount": 5000,
         "maxFollowersCount": 1000000
     }'
```

Replace `YOUR_CLIENTS_API_KEY` with your client's API key. Your clients can obtain their API key after subscribing to our platform by visiting this URL: https://app.spyfans.co/integrations

## Support

If you encounter any issues or have questions about integrating with our platform, please contact our support team on Telegram at [@spyfansupport](https://t.me/spyfansupport).
