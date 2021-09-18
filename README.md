# Animations

> #m-animate.keyframes(@name; @framelist; @frameprops)
> 
> Generates percentage-based keyframes.\
> > @param {name} Name of keyframes.\
> > @param {framelist} Comma-separated percentage values for each keyframe.\
> > @param {frameprops} Comma-seperated declaration list for each keyframe.

Example
```
  #m-animate.keyframes(
    fade;
    1, 100;
    { opacity: 0 },
    { opacity: 1 }
  );
```
Outputs
```
  @keyframes fade {
    0% {
      opacity: 0;
    }
    100% {
      opacity: 1;
    }
  }
```
---
> #m-animate.shorthand(@duration, @easing-function, @delay, @iteration-count, @direction, @fill-mode, @play-state, @name)
> 
> Accepts a named parameter matching each animation property.\
> > @param {duration} default 500ms\
> > @param {easing-function} default ease-in-out\
> > @param {delay} default 0s\
> > @param {iteration-count} default 1\
> > @param {direction} default normal\
> > @param {fill-mode} default forwards\
> > @param {play-state} default running\
> > @param {name} Name of keyframes. (required)

Example
```
  .bounce {
    #m-animate.shorthand(
      @name: pulse
      @duration: 250ms,
      @iteration-count: infinite
    );
  }
```
Outputs
```
  .bounce {
    animation: 250ms ease-in-out 0s infinite normal forwards running pulse
  }
```

# Transitions

> #m-transition.generate(@props, @delay, @duration, @timing, @onPsuedo, @onSelector, @from, @to)
> 
> Builds out transition properties and to/from style declarations for each style property passed in.\
> > @param {props} Comma-separated properties to transition i.e. background, font-size.\
> > @param {from} Comma-separated default style values for each property i.e. black, 12px.\
> > @param {to} Comma-separated transitioned style values for each property i.e. white, 18px.\
> > @param {delay} Comma-separated list of delay values for each property (default 0s).\
> > @param {duration} Comma-separated list of duration values for each property (default 500ms).\
> > @param {timing} Comma-separated list of timing-function values for each property (default ease-in-out).\
> > @param {onPsuedo} Value representing a psuedo selector for when the transition will apply i.e. hover, focus (default false).\
> > @param {onSelector} Escaped string representing a selector for when the transition will apply i.e. ~"&.is-animating" (default false).

Examples
```
  .btn--primary {
    #m-transition.genrate(
      @onPsuedo: hover;
      @props: background, color;
      @duration: 250ms, 500ms;
      @from: white, black;
      @to: black, white
    );
  }
  .btn--secondary {
    #m-transition.generate(
      @onSelector: ~"&.is-active";
      @props: border-color;
      @from: black;
      @to: blue;
    )

    border-style: solid;
    border-width: 2px;
  }
```
Outputs
```
  .btn--primary {
    transition-property: background, color;
    transition-delay: 0s;
    transition-duration: 250ms, 500ms;
    transition-timing-function: ease-in-out;
    background: white;
    color: black;
  }

  .btn--primary:hover {
    background: black;
    color: white;
  }

  .btn--secondary {
    transition-property: border-color;
    transition-delay: 0s;
    transition-duration: 500ms;
    transition-timing-function: ease-in-out;
    border-color: black;
    border-style: solid;
    border-width: 2px;
  }
  
  .btn--secondary.is-active {
    border-color: blue;
  }
```
