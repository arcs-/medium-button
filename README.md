# MediumButton
MediumButton extends your Medium Editor with the possibility to add more buttons.

You can still use the default buttons, MediumButton will just give you the abiity to add more and custom buttons

# Basic usage

![screenshot](https://raw.githubusercontent.com/arcs-/MediumButton/master/demo/screenshot.png)

Demo: [http://stillhart.biz/project/MediumButton/](http://stillhart.biz/project/MediumButton/)

### Installation

Download the [latest MediumEditor release](https://github.com/daviferreira/medium-editor/releases) 
Download the [latest MediumButton release](https://github.com/arcs-/MediumButton/releases) 

The next step is to reference the scripts

```html
<script src="js/medium-editor.js"></script>
<script src="js/MediumButton.min.js"></script>
```

### Usage

Follow the steps on the [MediumEditor Page](https://github.com/daviferreira/medium-editor)

Then you can then setup your custom buttons

HTML buttons
```javascript
// This creates a buttons which make text bold
'b': new MediumButton({label:'<b>B</b>', start:'<b>', end:'</b>'})


label: '<b>B</b>', // Button Label: HTML and Font-Awesome is possible  
start: '<b>',      // Beginning of the selection 
end:   '</b>'      // End of the selection 

```

JavaScript buttons
```javascript
// This creates a buttons which makes a popup
'pop': new MediumButton({label:'<b>Hello</b>', action: function(html, mark){alert('hello'); return html;}})


label: '<b>Hello</b>',          //Button Label -> same as in HTML button 
                                //Action can be an javascript function
action: function(html, mark){   //HTML(String) is the selected Text
           alert('hello :)');   //MARK(Boolean) is already marked
           return html;}        //never forget return new HTML!
        }						  

```

Add them to MediumButton
```javascript
 // Remember the indicator befor each Button
 // 'pop': new MediumButto...
 
 // add this to your 'buttons' just like a normal one

 buttons: ['pop', 'b', 'h2', 'warning']
 
 // add the code for the button as an extensions
 // Seperat them with a " , "
 
  extensions: {
        'b':  new MediumButton({label:'BOLD', start:'<b>', end:'</b>'}),
  }     
 
```

and you're done.

## Example

Remember to add a " , " between the buttons

```javascript
var editor = new MediumEditor('.editor', {
    buttons: ['b', 'h2', 'warning', 'pop'],
    extensions: {
        // Compacct
        'b':  new MediumButton({label:'BOLD', start:'<b>', end:'</b>'}),
        'h2': new MediumButton({label:'h2', start:'<h2>', end:'</h2>'}),

       // Expaned
       'warning': new MediumButton({
          label: '<i class="fa fa-exclamation-triangle"></i>',
          start: '<div class="warning">',
          end:   '</div>'
       }),
	   
	// With JavaScript
       'pop': new MediumButton({
          label:'POP', 
          action: function(html, mark){
                    alert('hello :)'); 
                    return html; 
                  }
        })
        
        
    }
});

```


# Syntax highlighting

Syntax highlighting is possible but not that easy(for now). You need to add an other Script like Prism or highlight.js. Here is an example for JavaScript with highlight.js.

```javascript
'JS': new MediumButton({
  label: '<i>JavaScript</i>',
  start: '<pre><code>',
  end: '</code></pre>',
  action: function(html, mark){
            if(mark) return '<!--'+html+'-->' + hljs.highlight('javascript', html.substring(3, html.length - 4).replace(/<\/p><p>/g, "\n").replace(/</g, "<").replace(/>/g, ">")).value;
            return html.split('-->')[0].split('<!--').join('');
          }
})
```
