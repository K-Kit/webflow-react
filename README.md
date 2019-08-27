# Overview

*Webflow React from Abruptive* is a CLI tool that helps designers & developers convert their Webflow projects to React. Inspired by Appfairy (Eytan Manor), the library is a continuation of Eythan's work, to provide an easier way to convert Webflow to React JS.

## Requirements

- Node.js

## Installation

`$ npm install abruptive/webflow-react -g`

## Getting Started

1. Install *Webflow React from Abruptive* by running the command above;
2. Setup your React project (e.g. by using create-react-app);
3. Export your Webflow site and add the files under `/.webflow` in your project;
4. Run the `webflow-react` command in your project root.
5. (Optional) Add `webflow-react` to your package.json scripts to render easier.

## Notes

Be sure to stash all your git changes as beforehand as Webflor React uses Git as a version control. 

After doing so you'll notice that a new git-commit has been created saying `Webflow React: Updated`. 

This commit includes all the changes that Webflor React has made, and shouldn't be edited or reworded.

## Methodology

Since machine generated assets aren't very easy to maintain due to their complexity, Webflow React takes on an old school approach where a single component is made out of a view and a controller. This way the view can be changed without us worrying about re-binding the event listeners and props.

- The view is automatically generated by Webflow React and shouldn't be changed, we treat it as a black box. 
- The controller however is user defined. 
- Every element within the controller is a proxy to an element within the view.

## Structure

The commit consists of the following files (regardless if they were added, modified or deleted):

- **public/** (public assets which should be served by our app's server)
  - **images/**
  - **fonts/**
  - **css/**

- **src/**
  - **scripts/** (scripts that should be imported in index.js)
  - **styles/** (css files that should be imported in index.js)
  - **views/** (contains ConsultFormView - further explanation below)

## Example

```js
import React from 'react'
import ConsultFormView from '../views/ConsultFormView'

class ConsultFormController extends React.Component {
  state = {}

  render() {
    return (
      <ConsultFormView>
        <name onChange={this.setName} />
        <phone onChange={this.setPhone} />
        <email onChange={this.setEmail} />
        <description onChange={this.setDescription} />
        <submit onClick={this.submit} />
      </ConsultFormView>
    )
  }

  setName = (e) => {
    this.setState({
      name: e.target.value
    })
  }
  setPhone = (e) => {
    this.setState({
      phone: e.target.value
    })
  }

  setEmail = (e) => {
    this.setState({
      email: e.target.value
    })
  }

  setDescription = (e) => {
    this.setState({
      description: e.target.value
    })
  }

  submit = () => {
    alert(`
      ${this.name}
      ${this.phone}
      ${this.email}
      ${this.description}
    `)
  }
}

export default ConsultFormController
```

## Configuration

The output can be controlled using a config file named `wfr.config.js` which should be located in the root of the project. The config file may (or may not) include some of the following options:

- **prefetch (boolean)** - Prefetch the styles and scripts which are necessary for the design to work. If not specified, the scripts and styles will be fetched during runtime.

- **source (source)** - Can either be set to `webflow`, `sketch` and represents the studio name that generated the basic CSS and HTML assets.

- **input (string)** - The input dir for the Webflow exported files. Defaults to `.webflow` dir in the root of the project.

- **output (string/object)** - If a string was provided, the output will be mapped to the specified dir. If an object, each key in the object will map its asset type to the specified dir in the value. The object has the following schema:
  - **public (string)** - Public dir. Defaults to `public`.
  - **src (string/object)** - Source dir. If a string is provided, all its content will be mapped to the specified dir, otherwise the mapping will be done according to the following object:
    - **scripts (string)** - Scripts dir. Defaults to `src/scripts`.
    - **styles (string)** - Scripts dir. Defaults to `src/styles`.
    - **views (string)** - Scripts dir. Defaults to `src/views`.

Alternatively, you may provide (extra) options through the command line like the following:

    $ webflow-react [...options]

## Command Options

Webflow React supports the following CLI options:

- **--prefetch**
- **--source/--src**
- **--input/--in**
- **--output/--out**
- **--config**

## More Resources

To learn more about how *Webflow React from Abruptive* works, check out the following resources provided by Eythan Manor for Appfairy, the original library Webflow React is based on:

- [Medium blog post](https://medium.com/@eytanmanor/how-to-create-a-react-app-out-of-a-webflow-project-309b696a0533) - An introduction to Eythan's Appfairy and the motives behind it.

- [YouTube video](https://www.youtube.com/watch?v=6hJe6pZld0o) - Eythan walking through Appfairy and an implementation of an example app.

- [Example app](https://github.com/DAB0mB/Appfairy/tree/master/examples/prefetch) - An example for a simple app which uses Eythan's Appfairy.

## Disclaimer

Webflow is a registered® trademarks of its respective holders. Its use does not imply any affiliation with or endorsement by them.

## License

Apache