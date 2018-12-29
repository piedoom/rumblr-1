## Intro

**Tumblr API for Rust**

#### Usage

E.g. [Create a new photo post](https://www.tumblr.com/docs/en/api/v2#post--create-a-new-blog-post-legacy):

```rust
extern crate rumblr;

use rumblr::TumblrClient;

fn main() {
    // OAUTH
    const CONSUMER_KEY: &'static str = "YOUR CONSUMER KEY";
    const CONSUMER_SECRET: &'static str = "YOUR CONSUMER SECRET";

    let client = TumblrClient::new()
        .set_consumer(CONSUMER_KEY, CONSUMER_SECRET)
        .proxy("http://127.0.0.1:1087")
        .unwrap()
        .oauth();

    client.save_keys("rumblr.keys").unwrap();

    // Already OAUTHed
    let client = TumblrClient::new()
        .proxy("http://127.0.0.1:1087")
        .unwrap()
        .load_keys("rumblr.keys")
        .unwrap();

    println!(
        "{:?}",
        client.legacy_post(
            "cestxavier.tumblr.com",
            None,
            None,
            None,
            None,
            None,
            None,
            None,
            rumblr::PostAction::New,
            rumblr::PostType::Photo {
                caption: None,
                link: None,
                source: Some("https://uvwvu.xyz/favicon.png"),
                data: None,
                data64: None,
            },
        )
    );
}
```

All client methods sync with [Tumblr API](https://www.tumblr.com/docs/en/api/v2).

#### TODO

Support [Neue Post Format](https://www.tumblr.com/docs/npf).
