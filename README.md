# Tryout WebComponents

This is an experiment on [Web Components](https://developer.mozilla.org/en-US/docs/Web/Web_Components) using [Svelte](https://svelte.dev).

*Note that you will need to have [Node.js](https://nodejs.org) installed.*


## Get started

Install the dependencies...

```bash
npm install
```

...then start [Rollup](https://rollupjs.org):

```bash
npm run dev
```

Navigate to [localhost:5000](http://localhost:5000) to see the component in use.

By default, the server will only respond to requests from localhost. To allow connections from other computers, edit the `sirv` commands in package.json to include the option `--host 0.0.0.0`.

## Components

### Number Input

This component will format inputted numbers into formatted number with thousand separators. This web component will fires event on update.

Element attributes:
- `name` - events fired from this element will be named `number-input-[event-type]--[name]`
- `value` - initial value for number input

Event Types:
- `update` - fires on update with with rawvalue inside event's detail