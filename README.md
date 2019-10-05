# React Workshop @ LinuxDays 2019

    2019 Ondrej Sika <ondrej@ondrejsika.com>
    https://github.com/ondrejsika/linuxdays2019-react


## Workshop Requirements

You have to have __Node.js__ & __Yarn__ installed. You also need text editor, I'll recommend you __VS Code__.

If you need help or ask any question, feel free to send me mail to <ondrej@sika.io>.

### Install on Mac

Using [Brew](https://brew.sh)

```
brew install node
brew install yarn
brew cask install visual-studio-code
```

### Install on Linux

- Node.js - <https://nodejs.org/en/download/package-manager/>
- Yarn - <https://yarnpkg.com/lang/en/docs/install>
- VS Code - <https://code.visualstudio.com/docs/setup/linux>


### Install on Windows

I don't recommed you Windows it self, but you can also setup envirenment there.

Using [Choco](https://chocolatey.org/)

```
choco install nodejs
choco install yarn
choco install vscode
```

## Example Project

<https://github.com/ondrejsika/jsemnela>


## Setup Project

### Gitignore

```gitignore
# .gitignore
node_modules
.next
out
.vscode
.DS_Store
```

### Editorconfig

```editorconfig
# .editorconfig
root = true
[*]
indent_style = space
indent_size = 2
charset = utf-8
trim_trailing_whitespace = true
insert_final_newline = true
end_of_line = lf
max_line_length = null
```

### Create package.json

```
yarn init
```

## Install React & Next.js

Install packages

```
yarn add next react react-dom
```

Add scripts to `package.json`

```json
...
  "scripts": {
    "dev": "next",
    "static": "next build && next export"
  }
...
```

### Create first page

Create file `./pages/index.js`

```js
export default () => {
  return <h1>Ahoy, I'm Nela!</h1>;
};
```

And run dev server

```
yarn dev
```

See <http://127.0.0.1:3000>

I can put there more text


```js
export default () => {
  return (
    <>
      <p>
        Ahoy, I'm Nela,
        <br />
        I'm half labrador half swiss shepard.
      </p>
      <p>
        I love watter (anytime, anywhere, dirty is better than clean), mud,
        mountines and play fetch.
      </p>
      <p>
        I was born 26th of May 2015 close to Hradec Kralove. Now, I live in
        Prague with my best owners Ondrej and Zuzka.
      </p>
    </>
  );
};
```


### next/head

If you want put something into `<head></head>` in HTML you can use next Head component.

```js
import Head from "next/head";

export default () => {
  return (
    <>
      <Head>
        <title>About me</title>
      </Head>
      ...
    </>
  );
};
```

### Add Another Page

Create file `./pages/contact.js`:

```js
import Head from "next/head";

export default () => {
  return (
    <>
      <Head>
        <title>Contact me</title>
      </Head>
      <p>
        I'm <a href="https://instagram.com/jsemnela">@jsemnela</a> on Instagram,
        you can write me there. You can also follow my owners{" "}
        <a href="https://instagram.com/ondrejsika">@ondrejsika</a> and{" "}
        <a href="https://instagram.com/zuzjes">@zuzjes</a>.
      </p>
    </>
  );
};
```

### next/link

We can add link between pages. If you use next Link component instead of a, links will support preloads.

Add those links to both pahes

```js
import Head from "next/head";
import Link from "next/link";

export default () => {
  return (
    <>
      ...
      <p>
        <Link href="/"><a>About me</a></Link>
        <br />
        <Link href="/contact"><a>Contact me</a></Link>
      </p>
      ...
    </>
  );
};
```

### Create own component

You see, we have same links on both pages, we can create own componet and use it in pages.

Create file `./components/Nav.js`

```js
// components/Nav.js
import Link from "next/link";

export default () => {
  return (
    <>
      <p>
        <Link href="/"><a>About me</a></Link>
        <br />
        <Link href="/contact"><a>Contact me</a></Link>
      </p>
    </>
  );
};
```

Now you can import your component and use it in pages.

```js
// pages/index.js
import Head from "next/head";
import Nav from "../components/Nav";

export default () => {
  return (
    <>
      <Head>
        <title>About me</title>
      </Head>
      <Nav />
      <p>
        Ahoy, I'm Nela,
        <br />
        I'm half labrador half swiss shepard.
      </p>
      <p>
        I love watter (anytime, anywhere, dirty is better than clean), mud,
        mountines and play fetch.
      </p>
      <p>
        I was born 26th of May 2015 close to Hradec Kralove. Now, I live in
        Prague with my best owners Ondrej and Zuzka.
      </p>
    </>
  );
};
```

### Add Bootstrap

You have to install plugins for CSS support

```
yarn add @zeit/next-css
```

You have to use this plugin in next config.

```js
// next.config.js

module.exports = {};

const withCSS = require("@zeit/next-css");
module.exports = withCSS(module.exports);
```

After change in next config, we have to restart next server.

Now web can use bootstrap (for css), because we work in react we also want react-bootstrap for (components):

```
yarn add bootstrap react-bootstrap
```

Now, we can import bootstrap css and use some react rootstrap compponents.

```js
// pages/index.js
import Head from "next/head";
import Nav from "../components/Nav";

import "bootstrap/dist/css/bootstrap.min.css";
import Container from "react-bootstrap/Container";

export default () => {
  return (
    <Container>
      <Head>
        <title>About me</title>
      </Head>
      <Nav />
      <p>
        Ahoy, I'm Nela,
        <br />
        I'm half labrador half swiss shepard.
      </p>
      <p>
        I love watter (anytime, anywhere, dirty is better than clean), mud,
        mountines and play fetch.
      </p>
      <p>
        I was born 26th of May 2015 close to Hradec Kralove. Now, I live in
        Prague with my best owners Ondrej and Zuzka.
      </p>
    </Container>
  );
};
```

You also have to add this bootstrap to second page.

### _app.js

If you dont want to repeat this bootstrap setting, navigation, ... layout it self, you can move those into `./pages/_app.js` and create layout for all your pages.

```js
// pages/_app.js
import App from "next/app";

import Nav from "../components/Nav";

import "bootstrap/dist/css/bootstrap.min.css";
import Container from "react-bootstrap/Container";

export default class MyApp extends App {
  render() {
    const { Component, pageProps } = this.props;
    return (
      <Container>
        <Nav />
        <Component {...pageProps} />
      </Container>
    );
  }
}
```

### Styles

You can add styles to components using prop `styles={{margin: '10px'}}` for example. You can also use component `<style jsx>` and `<style jsx global>`.

Put some styles to our layout.

```js
// pages/_app.js

import App from "next/app";

import Nav from "../components/Nav";

import "bootstrap/dist/css/bootstrap.min.css";
import Container from "react-bootstrap/Container";

export default class MyApp extends App {
  render() {
    const { Component, pageProps } = this.props;
    return (
      <Container style={{ maxWidth: "45em" }}>
        <Nav />
        <Component {...pageProps} />
        <p style={{ marginTop: "30px" }}>Made for LinuxDays 2019</p>
        <style jsx global>{`
          body {
            overflow-y: scroll;
          }
          p {
              font-size: 20px;
          }
        `}</style>
      </Container>
    );
  }
}
```

### Images

We also need plugin for images:

```
yarn add next-images
```

And setting in next config. Add to bootom of `next.config.js`.

```js
...

const withImages = require("next-images");
module.exports = withImages(module.exports);
```

Now you can import your images into JS.

We can create own Image component based on Bootstrap Image.

We can create `./components/Image.js` with:

```js
// components/Image.js

import React from "react";
import Image from "react-bootstrap/Image";

export default class MyImage extends React.Component {
  render() {
    return (
      <Image
        fluid={true}
        src={this.props.src}
        style={{ marginBottom: "30px" }}
      />
    );
  }
}
```

Now we can use this Image component in pages.

```js
// pages/contact.js
import Image from "../components/Image";
import Head from "next/head";

export default () => {
  return (
    <>
      <Head>
        <title>Contact me</title>
      </Head>
      <Image src={require("../data/ondzuznela.jpg")} />
      <p>
        I'm <a href="https://instagram.com/jsemnela">@jsemnela</a> on Instagram,
        you can write me there. You can also follow my owners{" "}
        <a href="https://instagram.com/ondrejsika">@ondrejsika</a> and{" "}
        <a href="https://instagram.com/zuzjes">@zuzjes</a>.
      </p>
    </>
  );
};
```

Now we can add image and Bootstrap grid into about me page:

```js
// pages/index.js

import Row from "react-bootstrap/Row";
import Col from "react-bootstrap/Col";
import Image from "../components/Image";
import Head from "next/head";

export default () => {
  return (
    <>
      <Head>
        <title>About me</title>
      </Head>
      <Row>
        <Col sm={6}>
          <Image src={require("../data/nela.jpg")} />
        </Col>
        <Col sm={6}>
          <p>
            Ahoy, I'm Nela,
            <br />
            I'm half labrador half swiss shepard.
          </p>
          <p>
            I love watter (anytime, anywhere, dirty is better than clean), mud,
            mountines and play fetch.
          </p>
          <p>
            I was born 26th of May 2015 close to Hradec Kralove. Now, I live in
            Prague with my best owners Ondrej and Zuzka.
          </p>
        </Col>
      </Row>
    </>
  );
};
```

### Improve Nav

We can make navigation prettier, we can create own button component based on Bootstrap button and use it there.

```js
// components/Button.js

import Button from "react-bootstrap/Button";
import Link from "next/link";

export default props => {
  return (
    <Link href={props.href}>
      <Button style={{ margin: "5px" }} variant="outline-primary">
        {props.children}
      </Button>
    </Link>
  );
};
```

Now we can improve Nav

```js
// components/Nav.js

import Button from "../components/Button";
import Row from "react-bootstrap/Row";
import Col from "react-bootstrap/Col";

export default () => {
  return (
    <Row style={{ marginBottom: "30px", marginTop: "30px" }}>
      <Col>
        <h1>@jsemnela</h1>
      </Col>
      <Col sm={8} style={{ textAlign: "right" }}>
        <Button href="/">About me</Button>
        <Button href="/gallery">Gallery</Button>
        <Button href="/contact">Contact</Button>
      </Col>
    </Row>
  );
};
```

### Gallery

We can create a simple gallery. We create Gallery component.

```js
// components/Gallery.js

import Row from "react-bootstrap/Row";
import Col from "react-bootstrap/Col";

import Image from "../components/Image";

export default () => {
  return (
    <Row>
      {this.props.images.map(image => {
        return (
          <Col sm={4}>
            <Image src={image} />
          </Col>
        );
      })}
    </Row>
  );
};
```

And use it in new page `pages/gallery.js`

```js
// pages/gallery.js

import Head from "next/head";
import Gallery from "../components/Gallery";

export default () => {
  return (
    <>
      <Head><title>@jsemela - About me</title></Head>
      <Gallery
        images={[
          require("../data/nela9.jpg"),
          require("../data/nela8.jpg"),
          require("../data/nela7.jpg"),
          require("../data/nela6.jpg"),
          require("../data/nela5.jpg"),
          require("../data/nela4.jpg"),
          require("../data/nela3.jpg"),
          require("../data/nela2.jpg"),
          require("../data/nela1.jpg")
        ]}
      />
    </>
  );
};
```

### Deploy

Install now

```
yarn add now
```

Add to scripts in package.json

```json
...
"scripts": {
  ...
  "now-build": "yarn run static",
  "deploy": "now",
  ...
}
...
```

Now you can deploy app into Zeit.co using:

```
now
```
