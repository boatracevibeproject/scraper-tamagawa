# BVP Tamagawa Scraper

[![tests](https://github.com/shimomo/bvp-tamagawa-scraper/actions/workflows/tests.yml/badge.svg)](https://github.com/shimomo/bvp-tamagawa-scraper/actions/workflows/tests.yml)
[![codecov](https://codecov.io/gh/shimomo/bvp-tamagawa-scraper/graph/badge.svg?token=E29OLT9UK5)](https://codecov.io/gh/shimomo/bvp-tamagawa-scraper)
[![php](https://poser.pugx.org/bvp/tamagawa-scraper/require/php)](https://packagist.org/packages/bvp/tamagawa-scraper)
[![stable](https://poser.pugx.org/bvp/tamagawa-scraper/v/stable)](https://packagist.org/packages/bvp/tamagawa-scraper)
[![unstable](https://poser.pugx.org/bvp/tamagawa-scraper/v/unstable)](https://packagist.org/packages/bvp/tamagawa-scraper)
[![license](https://poser.pugx.org/bvp/tamagawa-scraper/license)](https://packagist.org/packages/bvp/tamagawa-scraper)

BVP Tamagawa Scraper は、ボートレース多摩川の公式サイトから記者予想、オリジナル展示タイムをスクレイピングして取得できる PHP ライブラリです。

## 📦 Requirements
- PHP ^8.2
- Composer
- Carbon

## 💾 Installation
```bash
composer require bvp/tamagawa-scraper
```

## ⚡ Usage

### サポートメソッド一覧

| メソッド | 説明 | 引数 |
|---|---|---|
| `Scraper::scrapeForecasts($raceNumber, $raceDate = null)` | 記者予想を取得 | `$raceNumber` : 1〜12<br>`$raceDate` : Carbon対応日付文字列またはCarbonインスタンス（省略時は当日） |
| `Scraper::scrapeTimes($raceNumber, $raceDate = null)` | オリジナル展示タイムを取得 | 同上 |

**$raceDate の例**
- `'2025-01-01'`
- `'2025/01/01'`
- `'yesterday'`
- `Carbon::now()->subDay()`

### 基本的な使い方

```php
<?php

require __DIR__ . '/vendor/autoload.php';

use BVP\TamagawaScraper\Scraper;

// 記者予想を取得
$forecasts = Scraper::scrapeForecasts(1, '2024-01-03');

// オリジナル展示タイムを取得
$times = Scraper::scrapeTimes(1, '2024-01-03');

print_r($forecasts);
print_r($times);
```

### Scraper::scrapeForecasts()

```php
// 例: ボートレース多摩川の公式サイトから2024年01月03日の1レースの記者予想を取得
$forecasts = Scraper::scrapeForecasts(1, '2024-01-03');
print_r($forecasts);
```

<details>
<summary>取得結果</summary>

```php
Array
(
    [reporter_yesterday_comment_label] => 記者予想 前日コメント
    [reporter_yesterday_comment] => 開幕戦地元①相原利の逃げに懸ける。S奮起押し切るか。③青木蓮の25号機前回ターン系に好気配。握れる位置なら1M有利に行けそう。④佐藤航はそれを待つ形。
    [reporter_yesterday_course_label] => 記者予想 前日コース
    [reporter_yesterday_course] => 123/456
    [reporter_yesterday_focus_label] => 記者予想 前日フォーカス
    [reporter_yesterday_focus] => Array
        (
            [0] => 1=3
            [1] => 1-4
            [2] => 1=3-4
            [3] => 1-4-3
        )

    [reporter_yesterday_focus_exacta_label] => 記者予想 前日フォーカス 2連単
    [reporter_yesterday_focus_exacta] => Array
        (
            [0] => 1=3
            [1] => 1-4
        )

    [reporter_yesterday_focus_trifecta_label] => 記者予想 前日フォーカス 3連単
    [reporter_yesterday_focus_trifecta] => Array
        (
            [0] => 1=3-4
            [1] => 1-4-3
        )

    [jlc_yesterday_course_label] => JLC予想 前日コース
    [jlc_yesterday_course] => 123456
    [jlc_yesterday_focus_label] => JLC予想 前日フォーカス
    [jlc_yesterday_focus] => Array
        (
            [0] => 1-3-2
            [1] => 1-2-3
            [2] => 1-3-4
            [3] => 1-2-4
            [4] => 1-4-3
        )

    [jlc_yesterday_focus_exacta_label] => JLC予想 前日フォーカス 2連単
    [jlc_yesterday_focus_exacta] => Array
        (
        )

    [jlc_yesterday_focus_trifecta_label] => JLC予想 前日フォーカス 3連単
    [jlc_yesterday_focus_trifecta] => Array
        (
            [0] => 1-3-2
            [1] => 1-2-3
            [2] => 1-3-4
            [3] => 1-2-4
            [4] => 1-4-3
        )

    [jlc_yesterday_reliability_label] => JLC予想 前日信頼度
    [jlc_yesterday_reliability] => 55%
)
```

</details>

### Scraper::scrapeTimes()

```php
// 例: ボートレース多摩川の公式サイトから2024年01月03日の1レースのオリジナル展示タイムを取得
$times = Scraper::scrapeTimes(1, '2024-01-03');
print_r($times);
```

<details>
<summary>取得結果</summary>

```php
Array
(
    [boat_number_1_racer_name] => 相原利章
    [boat_number_1_racer_exhibition_time] => 6.7
    [boat_number_1_racer_lap_time] => 36.47
    [boat_number_1_racer_turn_time] => 6.07
    [boat_number_1_racer_straight_time] => 6.47
    [boat_number_2_racer_name] => 橋口真樹
    [boat_number_2_racer_exhibition_time] => 6.66
    [boat_number_2_racer_lap_time] => 36.97
    [boat_number_2_racer_turn_time] => 6.03
    [boat_number_2_racer_straight_time] => 6.68
    [boat_number_3_racer_name] => 青木蓮
    [boat_number_3_racer_exhibition_time] => 6.66
    [boat_number_3_racer_lap_time] => 36.7
    [boat_number_3_racer_turn_time] => 5.63
    [boat_number_3_racer_straight_time] => 6.93
    [boat_number_4_racer_name] => 佐藤航
    [boat_number_4_racer_exhibition_time] => 6.65
    [boat_number_4_racer_lap_time] => 36.44
    [boat_number_4_racer_turn_time] => 5.67
    [boat_number_4_racer_straight_time] => 6.87
    [boat_number_5_racer_name] => 田中勇輔
    [boat_number_5_racer_exhibition_time] => 6.68
    [boat_number_5_racer_lap_time] => 37.06
    [boat_number_5_racer_turn_time] => 5.57
    [boat_number_5_racer_straight_time] => 6.82
    [boat_number_6_racer_name] => 坂本一真
    [boat_number_6_racer_exhibition_time] => 6.72
    [boat_number_6_racer_lap_time] => 37.37
    [boat_number_6_racer_turn_time] => 5.93
    [boat_number_6_racer_straight_time] => 6.71
)
```

</details>

## ⚠️ Notes
- **スクレイピング対象の公式サイトの構造が変更された場合**、正しくデータを取得できなくなる可能性があります。
- 利用時は対象サイトの利用規約を遵守してください。

## 📄 License
BVP Tamagawa Scraper は [MIT license](LICENSE) の元で公開されています。
