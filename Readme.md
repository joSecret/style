Post CSS config:

### package.json

"path": "^0.12.7",
"postcss": "^8.4.47",
"postcss-advanced-variables": "^4.0.0",
"postcss-calc": "^10.0.2",
"postcss-cli": "^11.0.0",
"postcss-conditionals": "^2.1.0",
"postcss-custom-media-generator": "^1.1.0",
"postcss-each": "^1.1.0",
"postcss-import": "^16.1.0",
"postcss-mixins": "^11.0.1",
"postcss-nested": "^6.2.0",
"postcss-preset-env": "^10.0.3",
"postcss-pxtorem": "^6.1.0",
"postcss-replace-string": "^1.0.0",
"postcss-simple-vars": "^7.0.1",
"postcss-url": "^10.1.3",

drupal:
"chalk": "^4.1.2",
"chokidar": "^3.5.3",
"cssnano": "^5.1.14",
"fs-extra": "^10.1.0",
"glob": "^8.0.3",
"minimist": "^1.2.6",
"mkdirp": "^1.0.4",
"node-fs-extra": "^0.8.2",
"path": "^0.12.7",
"postcss": "^8.4.19",
"postcss-calc": "^8.2.4",
"postcss-cli": "^10.0.0",
"postcss-conditionals": "^2.1.0",
"postcss-dropunusedvars": "^1.2.1",
"postcss-advanced-variables": "^3.0.1",
"postcss-each": "^1.1.0",
"postcss-import": "^14.1.0",
"postcss-mixins": "^9.0.4",
"postcss-nested": "^6.0.0",
"postcss-preset-env": "^7.7.2",
"postcss-pxtorem": "^6.0.0",
"postcss-replace-string": "^1.0.0",
"postcss-url": "^10.1.3",

### postcss.config.cjs

const postcssAdvancedVar = require('postcss-advanced-variables');
const postcssCustomMediaGenerator = require('postcss-custom-media-generator');
const postcssNested = require('postcss-nested');
const postcssCalc = require("postcss-calc");
const postcssUrl = require('postcss-url');
const postcssPresetEnv = require('postcss-preset-env');
const postcssPixelsToRem = require('postcss-pxtorem');
const cssnano = require('cssnano');
const postcssEach = require('postcss-each');

module.exports = {
plugins: [
postcssAdvancedVar,

    postcssNested,

    postcssCustomMediaGenerator({
      "--light": "prefers-color-scheme: light",
      "--dark": "prefers-color-scheme: dark",
      sm: 576,
      md: 768,
      "--switchDown": "(max-width: 991px)",
      "--switchUp": "(min-width: 992px)",
      lg: 992,
      xl: 1200,
      xxl: 1400,
    }),

    postcssPresetEnv({
      stage: 2,
      preserve: false,
      autoprefixer: {
        cascade: false,
        grid: 'no-autoplace',
      },

      features: {
        'custom-properties': false,
        'blank-pseudo-class': false,
        'focus-visible-pseudo-class': false,
        'focus-within-pseudo-class': false,
        'has-pseudo-class': false,
        'image-set-function': false,
        'prefers-color-scheme-query': false,
        'logical-properties-and-values': false,
      }
    }),

    postcssCalc,

    postcssEach,

    postcssPixelsToRem({
      propList: [
        '*',
        '!background-position',
        '!border',
        '!border-width',
        '!box-shadow',
        '!border-top*',
        '!border-right*',
        '!border-bottom*',
        '!border-left*',
        '!border-start*',
        '!border-end*',
        '!outline*',
      ],
      mediaQuery: true,
      minPixelValue: 3,
    }),

    postcssUrl({
      filter: '**/*.svg',
      url: 'inline',
      optimizeSvgEncode: true,
    }),

    cssnano()

],
};
