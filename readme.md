# Web Components

#### by Alex Merced

## What are Web Components

Web Components allow you to do the same thing that Vue, Angular and React Components do... create encapsulated pieces of UI with their own internal logic, state and styling. The best part is you don't have to bring in a separate library to use Web Components although there are several libraries to make Web Components even easier to use (MercedUI, AMPonent, lit-html, StencilJS, Lightning Components).

## Let's Get Started

We are going to start very simple with just an `index.html` that looks like below:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>My Web Components</title>
  </head>
  <body>
    <h1>My Web Components</h1>

    <script></script>
  </body>
</html>
```

## The Basics

We need to do two things to create a web component

- Define the Component Class
- Register the Component with the Browser

### Defining the Component Class

To create a web component we will extend the class, HTMLElement.

```js
class FirstComponent extends HTMLElement {
  constructor() {
    super();
    this.innerHTML = `<h2>My First Component</h2>`;
  }
}
```

We define the constructor of the component where can define the html inside the component.

### Registering it with the Browser

The class needs to be registered with an HTML tag, which must be kebab case (kebab-case). We do this by using the customElements.define function which is passed the tag name and the class that is generated when that tag is used.

```js
class FirstComponent extends HTMLElement {
  constructor() {
    super();
    this.innerHTML = `<h2>My First Component</h2>`;
  }
}

customElements.define("first-component", FirstComponent);
```

### Using the Component

Now we can use the component in our html, in this case we've created a tag called `<first-component>`

```html
<h1>My Web Components</h1>
<first-component></first-component>
```

## Making it more dynamic

We can pass information to our component via custom attributes, this is usually referred to as "props" in React and Vue. So let's assume when we use this component we will pass in some custom text and color. We'll call them...

- mytext
- mycolor

So the end result will look like `<first-component mytext="text" mycolor="red"></first-component>`

So let's add the logic to pull these attributes to our custom component.

```html
<body>
  <h1>My Web Components</h1>
  <first-component mytext="text" mycolor="red"></first-component>

  <script>
    class FirstComponent extends HTMLElement {
      constructor() {
        super();
        const text = this.getAttribute("mytext");
        const color = this.getAttribute("mycolor");
        console.log(text, color);
        this.innerHTML = `<h2>My First Component</h2>`;
      }
    }

    customElements.define("first-component", FirstComponent);
  </script>
</body>
```

You should now see text and red being logged in the console. Let's use the component a few more times with different attributes.

```html
<h1>My Web Components</h1>
<first-component mytext="text" mycolor="red"></first-component>
<first-component mytext="another" mycolor="green"></first-component>
<first-component mytext="last" mycolor="purple"></first-component>
```

Now you should see three logs of the different properties, this shows us that each instance of the component has it's own state (data), a life of its own.

Now let's take those piece of information us them in our template.

```js
class FirstComponent extends HTMLElement {
  constructor() {
    super();
    const text = this.getAttribute("mytext");
    const color = this.getAttribute("mycolor");
    //   console.log(text, color)
    this.innerHTML = `<h2 style="color: ${color};">${text}</h2>`;
  }
}

customElements.define("first-component", FirstComponent);
```

You should be seeing colorful results on the screen.

## A more practical example... a fancy button

So let's build this component...

```js
class FancyButton extends HTMLElement {
  constructor() {
    super();
    const label = this.getAttribute("label");
    const style =
      "background-color: white; padding: 6px; border: 2px solid red; font-size: 20px;";
    this.innerHTML = `<button style="${style}">${label}</button>`;
  }
}

customElements.define("fancy-button", FancyButton);
```

Let's use it!

```html
<h1>My Web Components</h1>
<first-component mytext="text" mycolor="red"></first-component>
<first-component mytext="another" mycolor="green"></first-component>
<first-component mytext="last" mycolor="purple"></first-component>
<fancy-button label="add"></fancy-button>
<fancy-button label="subtract"></fancy-button>
```

## Bottom Line

This is only scratching the surface but imagine being able to have pre-designed buttons you can use from project to project, all you have to is sprinkle in a script tag and all these custom element become available pre-styled with useful logic. You can pre-build carousels, models, navigation bars and the only limit is your imagination.

If you want to learn more about web components check out the resources below which go deeper on the base syntax and over a couple of libraries that give you some extra features making building components even more similar to React or Vue.

## Additional Reading

- **Web Components Tutorial Part 1/3 -** https://tuts.alexmercedcoder.com/webcomp1/
- **Web Components Tutorial Part 2/3 -** https://tuts.alexmercedcoder.com/webcomp2/
- **Web Components Tutorial Part 3/3 -** https://tuts.alexmercedcoder.com/webcomp3/
- **MercedUI: Web Component Library Tutorial -** https://tuts.alexmercedcoder.com/mercedui/
- **AMPonent: Web Component Library Tutorial -** https://tuts.alexmercedcoder.com/amponenttut/
