# vue-invisible-recaptcha [![NPM version](https://badge.fury.io/js/vue-invisible-recaptcha.svg)](https://badge.fury.io/js/vue-invisible-recaptcha) [![Snippets Stats](https://codebottle.io/embed/search-badge?keywords=vue%20invisible%20recaptcha&language=6)](https://codebottle.io/?q=vue%20invisible%20recaptcha)

> Super easy Invisible Recaptcha integration with VueJS

> Library is kind of unstable. Bugs, missing features might be present


## Features
 - Good customizability
 - Automatically loads Google's scripts on-demand and only once
 - Automatic reset after callback execution
 - ..um it just works lol

## Installation

```bash
npm i vue-invisible-recaptcha --save
```

## Usage

Include the component,

```javascript
import InvisibleRecaptcha from 'vue-invisible-recaptcha';
```

Then, register the component, however you like:

```javascript
{
    ...
    components: {
        ...
        "invisible-recaptcha": InvisibleRecaptcha
    }
}
```

And then.. use the component:

```html
<invisible-recaptcha sitekey="..." :validate="prepare" :callback="doSomething"
    class="btn btn-danger" type="submit" id="do-something-btn" :disabled="loading">
    Do something!
</invisible-recaptcha>
```

Here's a detailed spec of every properties it accepts: (looks nicer on GitHub than NPM)

```
Prop name      =>    Description                         =>   Example

sitekey        =>    Client-side key from Google         =>   "some-fancy-id"
badge          =>    Badge location                      =>   "bottomright"
validate       =>    Func. executed before reCAPTCHA     =>   () => {this.loading = true}
                                                         =>   If this returns *exactly* false reCAPTCHA won't run
callback       =>    Func. executed after verification   =>   (recaptchaToken) => {console.log(recaptchaToken)}
disabled       =>    Whether the button is disabled      =>   true or false
id             =>    ID for the button                   =>   "do-something-btn"
type           =>    Button type (HTML5 prop)            =>   "submit"
```

There's a slot inside the button so you insert text or whatever. And yeah that's it, if there's something missing in the docs just look at the code, it's easy to understand.

**If you find any bug, please report it as soon as possible.** Contributions and pull requests are also highly appreciated as long as the code looks very clean, not over-complicated, and consistent.