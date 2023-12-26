---
title: 配置
---

您可以在 `_config.yml` 或 [替代配置檔](#Using-an-Alternate-Config) 中修改網站配置。

### 網站

| 設定            | 描述                                                                                                                                                                                                                                                                                        |
| ------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| `title`       | The title of your website                                                                                                                                                                                                                                                                 |
| `subtitle`    | The subtitle of your website                                                                                                                                                                                                                                                              |
| `description` | 網站描述                                                                                                                                                                                                                                                                                      |
| `keywords`    | The keywords of your website. Supports multiple values.                                                                                                                                                                                                                                   |
| `author`      | 您的名字                                                                                                                                                                                                                                                                                      |
| `language`    | The language of your website. 網站使用的語言，參考 [2-lettter ISO-639-1 code](https://en.wikipedia.org/wiki/List_of_ISO_639-1_codes)，預設為 `en` Default is `en`.                                                                                                                                      |
| `timezone`    | The timezone of your website. Hexo uses the setting on your computer by default. 網站時區，Hexo 預設使用您電腦的時區，您可以在 [時區列表](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones) 尋找適當的時區，例如 `America/New_York` 、 `Japan` 與 `UTC` Some examples are `America/New_York`, `Japan`, and `UTC`. |

### 網址

| 設定                           | 描述                                                             | Default                     |
| ---------------------------- | -------------------------------------------------------------- | --------------------------- |
| `url`                        | 網站的網址，must starts with `http://` or `https://`                 |                             |
| `root`                       | The root directory of your website                             | `url's pathname`            |
| `permalink`                  | 文章 [永久連結](permalinks.html) 的格式                                 | `:year/:month/:day/:title/` |
| `permalink_defaults`         | Default values of each segment in permalink                    |                             |
| `pretty_urls`                | 改寫 [`permalink`](variables.html) 的值來美化 URL                     |                             |
| `pretty_urls.trailing_index` | 是否在永久鏈接中保留尾部的 `index.html`，設置為 `false` 時去除                     | `true`                      |
| `pretty_urls.trailing_html`  | 是否在永久鏈接中保留尾部的 `.html`, 設置為 `false` 時去除 (_對尾部的 `index.html`無效_) | `true`                      |

{% note info 網站存放在子目錄 %}
如果您的網站存放在子目錄中，例如 `http://example.org/blog`，請將您的 `url` 設為 `http://example.org/blog` 並把 `root` 設為 `/blog/`。
{% endnote %}

範例:

``` yaml
# e.g. page.permalink is http://example.com/foo/bar/index.html
pretty_urls:
  trailing_index: false
# becomes http://example.com/foo/bar/
```

### 目錄

| 設定             | 描述                                                                                                                                                             | Default          |
| -------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------- |
| `source_dir`   | Source folder. Where your content is stored                                                                                                                    | `source`         |
| `public_dir`   | Public folder. Where the static site will be generated                                                                                                         | `public`         |
| `tag_dir`      | Tag directory                                                                                                                                                  | `tags`           |
| `archive_dir`  | Archive directory                                                                                                                                              | `archives`       |
| `category_dir` | 分類資料夾                                                                                                                                                          | `categories`     |
| `code_dir`     | Include code 資料夾                                                                                                                                               | `downloads/code` |
| `i18n_dir`     | i18n directory                                                                                                                                                 | `:lang`          |
| `skip_render`  | Paths that will be copied to `public` raw, without being rendered. 跳過指定檔案的渲染，您可使用 [glob 表達式](https://github.com/micromatch/micromatch#extended-globbing) 來配對路徑 |                  |

預設值

``` yaml
skip_render: "mypage/**/*"
# will output `source/mypage/index.html` and `source/mypage/code.js` without altering them.

## This also can be used to exclude posts,
skip_render: "_posts/test-post.md"
# will ignore the `source/_posts/test-post.md`.
```

### 寫作

| 設定                      | 描述                                                                                        | Default     |
| ----------------------- | ----------------------------------------------------------------------------------------- | ----------- |
| `new_post_name`         | The filename format for new posts                                                         | `:title.md` |
| `default_layout`        | Default layout                                                                            | `post`      |
| `titlecase`             | 把標題轉換為 title case                                                                         | `false`     |
| `external_link`         | Open external links in a new tab?                                                         |             |
| `external_link.enable`  | Open external links in a new tab?                                                         | `true`      |
| `external_link.field`   | Applies to the whole `site` or `post` only                                                | `site`      |
| `external_link.exclude` | Exclude hostname. Exclude hostname. Specify subdomain when applicable, including `www`    | `[]`        |
| `filename_case`         | 把檔案名稱轉換為: `1` 小寫或 `2` 大寫                                                                  | `0`         |
| `render_drafts`         | 顯示草稿                                                                                      | `false`     |
| `post_asset_folder`     | 啟動 [Asset 資料夾](asset-folders.html)                                                        | `false`     |
| `relative_link`         | 把連結改為與根目錄的相對位址                                                                            | `false`     |
| `future`                | 顯示未來的文章                                                                                   | `true`      |
| `highlight`             | 程式碼區塊的設定, see [PrismJS](/docs/syntax-highlight#PrismJS) section for usage guide           |             |
| `prismjs`               | 程式碼區塊的設定, see [Highlight.js](/docs/syntax-highlight#Highlight-js) section for usage guide |             |

### Home page setting

| 設定                               | 描述                                                                                                              | Default |
| -------------------------------- | --------------------------------------------------------------------------------------------------------------- | ------- |
| `index_generator`                | Generate an archive of posts, powered by [hexo-generator-index](https://github.com/hexojs/hexo-generator-index) |         |
| `index_generator.path`           | Root path for your blog's index page                                                                            | `''`    |
| `index_generator.per_page`       | Posts displayed per page.                                                                                       | `10`    |
| `index_generator.order_by`       | Posts order. Order by descending date (new to old) by default.                                                  | `-date` |
| `index_generator.pagination_dir` | URL format, see [Pagination](#Pagination) setting below                                                         | `page`  |

### 分類 & 標籤

| 設定                 | 描述                 | Default         |
| ------------------ | ------------------ | --------------- |
| `default_category` | 分類別名               | `uncategorized` |
| `category_map`     | 預設分類               |                 |
| `tag_map`          | Override tag slugs |                 |

分頁目錄

``` yaml
category_map:
  "yesterday's thoughts": yesterdays-thoughts
  "C++": c-plus-plus
```

### 日期 / 時間格式

Hexo 使用 [Moment.js](http://momentjs.com/) 來解析和顯示時間。

| 設定               | 描述                                                                                              | Default      |
| ---------------- | ----------------------------------------------------------------------------------------------- | ------------ |
| `date_format`    | 日期格式                                                                                            | `YYYY-MM-DD` |
| `time_format`    | 時間格式                                                                                            | `HH:mm:ss`   |
| `updated_option` | The [`updated`](/zh-tw/docs/variables#頁面變數) value to used when not provided in the front-matter | `mtime`      |

{% note info updated_option %}
`updated_option` controls the `updated` value when not provided in the front-matter:

- `mtime`: Use file modification date as `updated`. It is the default behavior of Hexo since 3.0.0 It is the default behavior of Hexo since 3.0.0
- `date`: Use `date` as `updated`. `date`: Use `date` as `updated`. Typically used with Git workflow when file modification date could be different.
- `empty`: Simply drop `updated` when not provided. May not be compatible with most themes and plugins. May not be compatible with most themes and plugins.

`use_date_for_updated` is removed in v7.0.0+. Please use `updated_option: 'date'` instead.
{% endnote %}

### 分頁

| 設定               | 描述                                                              | Default |
| ---------------- | --------------------------------------------------------------- | ------- |
| `per_page`       | Number of posts displayed on each page. 一頁顯示的文章量 (`0` = 關閉分頁功能) | `10`    |
| `pagination_dir` | URL format                                                      | `page`  |

範例:

``` yaml
pagination_dir: 'page'
# http://example.com/page/2

pagination_dir: 'awesome-page'
# http://example.com/awesome-page/2
```

### 擴充套件

| 設定               | 描述                                                                                                                                      |
| ---------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| `theme`          | Theme name. `false` disables theming                                                                                                    |
| `theme_config`   | Theme configuration. Include any custom theme settings under this key to override theme defaults.                                       |
| `deploy`         | 佈署設定                                                                                                                                    |
| `meta_generator` | [Meta generator](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/meta#Attributes) tag. `false` disables injection of the tag. |

### 包含/排除 檔案或資料夾

Use the following options to explicitly process or ignore certain files/folders. Support [glob expressions](https://github.com/micromatch/micromatch#extended-globbing) for path matching.

`include` and `exclude` options only apply to the `source/` folder, whereas `ignore` option applies to all folders.

| 預設值       | Description                                                                                                  |
| --------- | ------------------------------------------------------------------------------------------------------------ |
| `include` | Include hidden files (including files/folders with a name that start with an underscore, with an exception*) |
| `exclude` | 原始檔案資料夾，這個資料夾用於存放您的內容                                                                                        |
| `ignore`  | Ignore files/folders                                                                                         |

auto_spacing

```yaml
# 包含/排除 檔案或資料夾
include:
  - ".nojekyll"
  # 包括 'source/css/_typing.css'
  - "css/_typing.css"
  # 包括 'source/_css/' 中的任何文件，但不包括子目录及其其中的文件。
  - "css/_typing.css"
  # Include any file in 'source/_css/'.
  - "_css/*"
  # Include any file and subfolder in 'source/_css/'.
  - "_css/*"
  # 包含 'source/_css/' 中的任何文件和子目录下的任何文件
  - "_css/**/*"

exclude:
  # 不包括 'source/js/test.js'
  - "js/test.js"
  # 不包括 'source/js/' 中的文件、但包括子目录下的所有目录和文件
  - "js/*"
  # 不包括 'source/js/' 中的文件和子目录下的任何文件
  - "js/**/*"
  # 不包括 'source/js/' 目录下的所有文件名以 'test' 开头的文件，但包括其它文件和子目录下的单文件
  - "js/test*"
  # 不包括 'source/js/' 及其子目录中任何以 'test' 开头的文件
  - "js/**/test*"
  # 不要用 exclude 来忽略 'source/_posts/' 中的文件。
  - "js/test.js"
  # Exclude any file in 'source/js/'.
  - "js/*"
  # Exclude any file and subfolder in 'source/js/'.
  - "js/**/*"
  # Exclude any file with filename that starts with 'test' in 'source/js/'.
  - "js/test*"
  # Exclude any file with filename that starts with 'test' in 'source/js/' and its subfolders.
  - "js/**/test*"
  # Do not use this to exclude posts in the 'source/_posts/'.
  # Use skip_render for that. Or prepend an underscore to the filename.
  # - "_posts/hello-world.md" # Does not work.

ignore:
  # Ignore any folder named 'foo'.
  ignore:
  # Ignore any folder named 'foo'.
  - "**/foo"
  # Ignore 'foo' folder in 'themes/' only.
  - "**/themes/*/foo"
  # Same as above, but applies to every subfolders of 'themes/'.
  - "**/themes/**/foo"
  - "**/themes/*/foo"
  # Same as above, but applies to every subfolders of 'themes/'.
  - "**/themes/**/foo"
```

Each value in the list must be enclosed with single/double quotes.

`include` 和 `exclude` 並不適用於 `themes/` 目錄下的文件。 如果需要忽略 `themes/` 目錄下的部分文件或文件夾，可以使用 `ignore` 或在文件名之前添加下劃線 `_`。

\* Notable exception is the `source/_posts` folder, but any file or folder with a name that starts with an underscore under that folder would still be ignored. Using `include:` rule in that folder is not recommended.

### 使用替代配置檔

使用 `hexo` 指令時，只要在指令後面加上 `--config` 參數與自訂配置檔 (需為 JSON 或 YAML 檔) 路徑即可指定此次想要搭配使用的配置檔。 該參數也可以是以逗號分隔的檔案列表 (注意中間不得有空格) 來滿足一次使用多個配置檔的需求。

``` bash
# 使用自訂的 'custom.yml' 取代預設的 '_config.yml'
$ hexo server --config custom.yml

# 使用多個配置檔, 有衝突時優先使用 'custom2.json'
$ hexo server --config custom.yml,custom2.json
```

使用多個配置檔會合併產生一個 `_multiconfig.yml`。 當合併遇到衝突時，列在愈後面的檔案，有愈高的優先權。 可以使用任意數量帶有任意層級物件的 JSON 或 YAML 檔。 注意**檔案列表字串中不得有空白**。

以前述的多個配置檔範例來說明，若 `custom.yml` 中有 `foo: bar`，且 `custom2.json` 中有 `"foo": "dinosaur"`，最終在 `_multiconfig.yml` 裡的將會是 `foo: dinosaur`。

### Alternate Theme Config

Hexo themes are independent projects, with separate `_config.yml` files.

Instead of forking a theme, and maintaining a custom branch with your settings, you can configure it from somewhere else.

**`theme_config` in site's primary configuration file**

> Supported since Hexo 2.8.2

```yml
# _config.yml
theme: "my-theme"
theme_config:
  bio: "My awesome bio"
  foo:
    bar: 'a'
```

```yml
# themes/my-theme/_config.yml
bio: "Some generic bio"
logo: "a-cool-image.png"
  foo:
    baz: 'b'
```

Resulting in theme configuration:

```json
{
  bio: "My awesome bio",
  logo: "a-cool-image.png",
  foo: {
    bar: "a",
    baz: "b"
  }
}
```

**dedicated `_config.[theme].yml` file**

> Supported since Hexo 5.0.0

The file should be placed in your site folder, both `yml` and `json` are supported. The file should be placed in your site folder, both `yml` and `json` are supported. `theme` inside `_config.yml` must be configured for Hexo to read `_config.[theme].yml`

```yml
# _config.yml
theme: "my-theme"
```

```yml
# _config.my-theme.yml
bio: "My awesome bio"
foo:
  bar: 'a'
```

```yml
# themes/my-theme/_config.yml
bio: "Some generic bio"
logo: "a-cool-image.png"
  foo:
    baz: 'b'
```

Resulting in theme configuration:

```json
{
  bio: "My awesome bio",
  logo: "a-cool-image.png",
  foo: {
    bar: "a",
    baz: "b"
  }
}
```

{% note %}
We strongly recommend you to store your theme configuration in one place. We strongly recommends you to store your theme configuration in one place. But in case you have to store your theme configuration separately, those information is quite important: The `theme_config` inside site's primary configuration file has the highest priority during merging, then the dedicated theme configuration file, while the `_config.yml` file under the theme directory has the lowest priority. The `_config.yml` file under the theme directory has the lowest priority.
{% endnote %}
