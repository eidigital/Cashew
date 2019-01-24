# Cashew
A simple PHP wrapper to make Instagram API call and cache the result

### Requirements

- PHP 5.3 or higher
- cURL
- Registered Instagram App

### Usage

This is a simple script for making API calls to `/users/user-id/media/recent` Endpoint. The main purpose of writing this wrapper was to get the latest images on user's feed.

### Do I need this?

If you are trying to get the data from a public username, you might be able to only use Instagram web interface by adding `/?__a=1` at the end of the profile's URL. (at present time of writing)

i.e: [https://www.instagram.com/amirandalibi/?__a=1](https://www.instagram.com/amirandalibi/?__a=1)

But if you are trying to get access to a private user info, You will need this.

### How does the caching work?

Since the API has `500` rate limit per hour, it's best to cache the result to reduce the calls. The default cache time is an hour which you can change in `cache.php`

This script will store the API response in `_cache` folder with the filename that you defined as `label` using native PHP function `file_put_contents()`. The `_cache` folder path should be explicitly set in the theme directory when initializing the class.

### Authorization flow

In order to use this script you need to create an app in your account and obtain an access token.

Every new app created on the Instagram Platform starts in Sandbox mode. and they are restriced to 10 users and the 20 most recent media from each of those users.

### Initialize the class

```php
use Accolade\Cashew\InstagramOAuth;

$instagram = new InstagramOAuth;
$instagram->get_feed(
  $PathforCacheFolder,
  $LabelforCashedFilename,
  $AccessToken
);

```

This will return the API data `json_decode()` - so you can directly access the data.
