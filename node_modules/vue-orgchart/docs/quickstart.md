## Quick Start

### Install
```shell
npm install vue-orgchart -S
```

### Import in your project

> `main.js`

```js
import 'vue-orgchart/dist/style.min.css'
```

> In `*.vue`

```js
<vo-basic :data="chartData"></vo-basic>
import { VoBasic } from 'vue-orgchart'
export default {
  components: { VoEdit },
  created () {
    this.chartData = {
      name: 'JavaScript',
        children: [
          { name: 'Angular' },
          {
            name: 'React',
            children: [{ name: 'Preact' }]
          },
          {
            name: 'Vue',
            children: [{ name: 'Moon' }]
          }
        ]
    }
  }
}
```

### CDN
```html
<link rel="stylesheet" href="https://cdn.jsdelivr.net/npm/vue-orgchart/dist/style.min.css">
<script src="https://cdn.jsdelivr.net/npm/vue-orgchart/dist/vue-orgchart.min.js"></script>
```
