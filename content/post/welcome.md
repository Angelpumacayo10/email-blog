+++

title = "Fundamentals of building Email Templates"
date = "2016-11-09T13:34:21-08:00"

+++



### Important when designing HTML Emails:



* Should be 600-800 pixels maximum width.
* Design for Simplicity.
* Emails that are one large image perform poorly.
* Use basic, cross platform fonts; Arial, Verdana, Georgia, Times New Roman.
* Avoid elements that require FLASH or JS, if you need motion in your email, a .gif is your best bet.
* Mobile experience is key, email has to be readable on small screens and make sure links are easy to press with thumb.



### Best Development Practices:


 * Code all structure using table elements, for more complicated layouts nest tables to build complex structures.
 * Element attributes, (cellpadding, align, width) to set table dimensions. This forces a box-model structure.
 * Keep CSS simple, avoid compound style declarations: (IE: “font: #000 1px Arial, Helvetica, Sans-Serif;”).
 * Avoid CSS layout properties (IE: slot, position, clear, visibility etc).
 * Avoid complex selectors (IE: descendant, child, or sibling selectors, and pseudo elements).
 * Inline all CSS before sending (Some builders will do this for you automatically : Mailchimp).
 * Use absolute links for images and host those images on a reliable server(Mailchimp provides free image hosting).
 * Don’t bother with Javascript or FLASH. Those technologies are largely unssupported by email clients.
 * Account for mobile-friendliness.
 * Use media queries to increase text size on small screens, provide thumb-sized (46px-46px) hit areas for links.
 * Make an email responsive if the design allows it.
 * TEST, TEST, TEST. Create email accounts across various services, and send emails to yourself. Do this is conjunction with services such as litmus.




### Building an HTML Email:




Before we begin you will need a working knowledge of HTML, CSS, media queries and the use of some external resources. At its core an HTML email is an HTML file, the code that we write is viewed in email clients, in which you would visit a Url like gmail.com to acess your email or yahoo.com to acess your yahoo mail. The other type of clients are native applications, one popular version of this for microsoft operating systems is called Microsoft Outlook and for IOS clients is the mailbox application.


In modern front-end development we are used to writing code that is viewed in browsers, those browsers use rendering engines to interpret the HTML and CSS that we write, email clients have this same process but they have an additional step too, they use a pre-processor that will actually change your HTML. The original purpose for a processor is to protect the client from harmful code, now pre-processors are your strongest opponents, they:


* Removes or changes HTML tags
* Removes or changes CSS
* Overrides styles with APP CSS
* Changes the entire document structure
* Removes all Javascript.


Gmail has the most aggressive pre processor of all, very unfortunate because it’s one of the most popular email clients out there. The combination of its popularity and pre processor affects the way you have to write your HTML and CSS. This is what Gmails pre processor does:


* Removes any link tags, this means if you have any external style sheets, they would be removed.
* Overrides styles with its own version; APP CSS.
* Changes the entire document structure.
* Removes style tags - this means that we can’t CSS in an external stylesheet, and you also can’t lump together CSS properties in a style tag to apply to HTML elements.


Let’s get started, this would be the start of your basic HTML email:


``` html
<!DOCTYPE html>
  <head>
    <meta charset="utf-8">
    <title> San Jose Earthquakes Try Outs </title>
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <meta http-equiv="X-UA-compatible" content="IE-edge" />
  </head>

  <body style="margin: 0; padding: 0;">
    <img src=”http://images.footballfanatics.com/partners/MLS/San%20Jose%20Earthquakes/MLS_TLP_Header_Earthquakes4.jpg” alt=”Earthquakes Online Store Webstie Logo“ width=”600” >
  </body>
</html>
```


Note that every time you are adding an image to an HTML email, you need to use an absolute Url, the image needs to be stored in an a server and accessible, you can reference to it by using an absolute path, this is one big difference between email HTML and website HTML, all of the the images should have an absolute Url. To add writing or content to the page you can use the h1 and p tags.


When building an HTML email it is really important to stay organized, i cannot emphasize this enough, you really want to stay organized. To stay organized i would suggest leaving comments on top of your tables or divs. It is best practice for HTML email developers to do this, use a comment to indicate what the table below is for, it can be a comment to give you an idea of what the code below is referencing, something to help you and maybe someone you are working with stay organized. This makes it easy to scan your code your code and believe me it will help you in the long run because HTML table can get really bloated, and you can get lost in this code at times.


Knowing what pre processors are capable of, and since you don’t have support for external stylesheets or style tags, inline styles must be used. This is how you would add inline attributes to an image tag:



``` html
<img src=”img/quakes.jpg”
  style='
    background-color: #123332;
    display: block;
    max-width: 100%;
    padding: 12px 0;
    width: 600
  '
/>
```

You can add CSS attributes with CSS properties inline, it would be the same process to add it to an h1 tag, let me show you:


``` html
<h1 style='
  color: #845679;
  font-family; ‘Arial Black’;
  font-size; 74px;
  line-height; 74px;
  margin: 0;
  text-transform: uppercase; '>
  Email Title</h1>
```

One thing to note is that because you can’t reference an area of CSS, we have to include any reset styles to very element that we want to reset. Margin: 0; would counter any browser behavior that would add spacing to our h1 tag.


Another problem that you will encounter will be that you will want the content of your elements to be aligned and have equal widths, you can fix this by adding a div around all of your current content and apply as follows:


``` html
<div style='
  margin: 0 auto;
  max-width: 600px; '>
 <img……>
 <h1……>
 <p…>
</div>
```

Margin: 0 auto; to center everything and applying max-width so that it never gets bigger 600 pixels. You can also add the text-align attribute to your div so that it can cascade down to all of the text inside the div.


To add a background you will need to add a div around your current content container and apply a background color and background image as follows:


``` html
<div style='
      background-color: #444544;
      background-image: Url(“... bgimage.png”); '>
    <div ……>
    <img……>
    <h1 ……>
    <p ………>
   </div>
  </div>
```

### MICROSFT OUTLOOK:


Outlook 2003-2013 use different rendering engines, prior to 2007 word used internet explorer for its rendering engine, 2007 and later uses microsoft word. Word lacks box mode and positioning support, everything that you could think of that you would use to create a layout in CSS is not supported by it, let me show you what outlook does not support:


``` html

              Height | Display | Float | Position | Width | Padding
     Outlook         |         |       |          |       |
    2007-2013    X   |   X     |   X   |    X     |  !!!  |  !!!

```


As you can see outlook gives us little to work with and the width and padding are only supported on table elements. You should absolutely avoid using tables for layouts when building web pages, however they are a necessity for HTML emails because of the lack of CSS support.
Table usually use many semantic elements to create their structure, however that would be too much code than you would actually need for your layouts, it’s better to use simplified tables. For the majority of the time you will only need to use table elements, table row elements and table cell elements.


       <!--WRAPPER HEADER-->

        <table border=”0” cellpadding=”0” cellspacing=”0”>
          <tr>
            <td>
              <!---content--->
            </td>
          </tr>
        </table>


Many clients apply default spacing in order to space out tables, in order to counter this you will need to use HTML attributes and them add to the table as shown up top. ALL TABLES WILL NEED TO HAVE THESE RESET ATTRIBUTES.


All of the content must go in a table cell, the word rendering engine has very minimal support for styles on any HTML elements except for the table and table cell, this means we need to divide our content into individual table in order for them be styled, like this:

``` html
       <table … width=”600” >
         <tr>
          <td style=”
              background-color: #577374;
              padding: 12px 0; “>
       <img src=”…..groundimage.png”
             style=”
              display: block;
              max-width : ”100%";
              width=”600” />
          </td>
         </tr>
         <tr>
           <td style=”
                color: #754674;
                font-family: ‘Arial Black’;
                font-size: 74px;
                line-height: 74px;
                padding: 5px 0 10px 0;
                text-transform: uppercase;>
           San Jose Earthquakes Try Outs!</td>
         </tr>
```

Earlier we applied our styles to the image tag, however to get the best support we want to apply our bgcolor and padding to the, type styles need to be applied to the table cell. One nice thing is that you don’t have to include any reset CSS because we are not getting any default styles applied to our table cell.


Like before we are going to apply our text-align: center to our containing element. The reason why we are not bringing our font styles to the table level to only be set once is because different rendering engines set default styles to the table cells, chrome sets font-family to Arial, AOl goes ahead and sets the color black on td’s. In table elements you can use the align attribute to center all the content. Now to add a background to our layout you will need to wrap the table with all of your content inside of another table and add the background to the new table like this:

``` html
       <body……>
        <table…
           style=”
           background-color: #547389;
           background-image : Url(“bd-example.png”); “
           width=”100%” >
        <tr>
         <td>
        <table …..>  ← content table
         </td>
        </tr>
         </table>
        </body>
```


REMEMBER TO ALWAYS KEEP TESTING YOUR WORK WITH DIFFERENT EMAIL CLIENTS.


Multiple tables and nested tables help to build a layout, it is important to know that each section needs a new table, you can use nested tables inside tables if you have more than 1 content area. If you wanted to create space between the header and the tables below, you would usually use margin, however you get varied result in clients when using margin and outlook.com specifically doesn’t support it, instead you can use padding.

``` html

       <tr>
        <td style=”padding-top: 25px; “>
       <img …….>
        </td>
       </tr>
```

To create a table with 2 columns you can use a wrapper table with 2 cells to align the content, the default behavior will align them side by side. Remember that the content in the column needs to be in its own table for styling, you can use cellpadding to separate the 2  columns.

``` html
       <table…….>
        <tr>
         <td style=”padding-right: 10px;”>
       <table bgcolor=”#654434” …...>
          ……..
         </td>
         <td style=”padding-left: 10px;” >
       <table bgcolor=”#544544” style=” ……”
             width=”290”>
        <tr>
         <td>
       <img ….. />
         </td>
        </tr>
       </table>
         </td>
```

Remember styles are applied to the cells for each bit of content. To style a cell with multiple font sizes and styles you will need to wrap a span around each area of the text that you want to be styled differently. Here is an example:

``` html
       <tr>
        <td style=”
             font-family : Arial;
             font-size: 14px;
             font-weight: bold;
             line-height: 14px;
             padding-top: 5px; “>
        <span style=”
              font-family: ‘Arial Black’;
              font-size: 28px;
              line-height: 28px; “>
           Ages 14-24</span>
        <span style=”
              font-family: ‘Arial Black’;
              font-size: 30px;
              line-height: 30px; “>
         $100 Fee</span>
         Open to public
         </td>
       </tr>
```

REMEMBER TO KEEP TESTING YOUR WORK IN DIFFERENT RENDERING ENGINES!! ITS VERY IMPORTANT!.


### Using Media Queries:


The basic use of media queries in HTML emails would be to adjust your layout for smaller screens. Let’s say you are using a 600px wide table but you only have a 320px container, it just would not fit, the solution for that would be to use CSS to force the width of the table to be 100% of the container. This would be ok because any client that would support media queries would also support CSS in a style tag. Once we create a rule we can apply that rule to each table using a class attribute. While we would want these styles to apply to any client that does support media queries, we don’t want it to always impact our tables, we only want this width of 100% to apply when our screen is less than 600 pixels, so as you can see in the code below i added a media query with a max-width of 600 pixels to hold that rule.

``` html
       <head>
        <style>
         @media screen and(max-width: 600px) {
         .width-full {
          width: 100% !important; } }

             </style>
        </head>
                ……….
        <body ……>
        <table…… class=”width-full” ”width=”600” >
                ………….
        <table…… class=”width-full” ”width=”600” >
                ………….
        <table…… class=”width-full” ”width=”600” >
                ………….
        </body>
```


Another problem you will run into will be having to stack columns on small screens, this usually happens when you have multiple table cells in a row that won’t all fit in one row on a small screen, you will need a way to override the default behavior for the table cells. For this you will need to add a class to the table cells and on the style tag use the proper attributes to force stacking and use 100% of the width. Once your table cells are stacked on top of each other you will noticed that they are not aligned, there seems to be a problem with the padding, this is because of the padding that we added for the 600 pixels layout, it will affect the way it renders in small screens, you will need to override this, to do this all you will need to do is reset the padding for that table cell with the “ !important “ declarative. Below is an example of how to handle these 2 problems:

``` html
       <style>
         @media screen and (max-width: 600px){
           …..
         .stack-column {
            display: block !important;
            padding: 0 !important;
            width: 100%; }
        </style>
           …..
        <body>
          ……...
        <table….. class=”width-full” width=”600” >
          <td class=”stack-column”
              style=” padding-right: 10px; “>
             …………..
          <td class=”stack-column”
              style=” padding-right: 10px; “>
             ………
```

There will be times when you get inconsistent results with your font-family, it’s usually because the font you choose might not be available on all operating systems, for this you will need to create fallbacks. The fallbacks will need to be updated on every cell and span that contains a font-family. Here is an example of how to use fallbacks:


``` html
          ………
       <td style= “ ….
            font-family: “Arial” , “Arial Black” ,
            “Arial Bold” , “sans-serif”; … “>
       Soccer Tryouts!!</td>
```


Don’t forget to add it to every cell and span, it is a long process but using classes, attributes, and declarations would be how to adjust your layout for other platforms and small screens. You will need to target a client and override their multiple properties using classes to target what you want to override and attributes with the “!important” declaration to make sure it renders properly.
Like i mentioned before Word and Outlooks rendering engines have many issues, but lucky for us there are specific ways for us to target individual Outlook clients and its versions, to target all versions of Microsoft Outlook you can use a conditional comment and to target a specific version of Outlook you can use an operator.


``` html
       <!-- [if mso]>             <!--[if gte mso 11]>
            ……                         ……..
         <![endif]-->               <![endif]-->


      -Conditional Comment-           -Operator-
```



The gte operator on the top right will target Microsoft Outlook versions 2011 and higher. Inside conditional comments you can override attributes using classes to fix the layout of the specific client you’re targeting.


``` html
       <!--[if gte mso 11]>
        <style>
         .email-header {
           padding-bottom: 0 !important;   }
        </style>
       <![endif]-->
```





Microsoft Word Processor ignores line-height on inline elements.
Use &nbsp for empty cells or else the empty cells will be applied default settings.
Keep testing and always use HTML attributes when possible, that’s going to give you the best rendering across all different clients.




 Adding a button to your email:


Now to keep adding content to our email we are going to add a button that will work in multiple clients, typically the way you would add a button would be to create an anchor tag and add a bunch of styles to it. This would work in any clients that would use browser based rendering engines but it would not work on the Word rendering engine, the way i learned how to is actually pretty simple, fast, and effective. There is an excellent resource online created by stig at campaign monitor, buttons.cm generates code for the button with a conditionalcomment for using VML(Vector Markup Language). Buttons.cm allows you to create a button using inner values and outputs 2 versions of a button, one that would use VML and HTML that would render in the Word rendering engine, and one using just HTML to render in all other rendering engines. It is pretty simple to use, the first step would be to put the code for the button into a table cell on our email, once you add the code i would recommend to test it right away to see how it renders in multiple clients. If you’re having a consistent experience but it does not match your design exactly how you want it to you will need to go through a two step process to edit and style the button. The first step would be to set styles on the center tags, once you apply your styles and make your changes i recommend to test it on different rendering engines again, you should notice that these changes are only taking place on clients using the Word rendering engine. These changes are only visible in Outlook using Word because the VML is wrapped around a conditional tag that is targeting specifically microsoft Outlook. Here below is an example of how this would look like:


``` html
       <td …….. >
         <!--[if mso]>
          <v:roundrect …..
            ………..
       <center style=” color: #ffffff;
                font-family: Arial, sans serif;
                font-size: 22px;
                font-weight: bold;
                text-transform: uppercase; “>
         Buy Tickets </center>
           </v:roundrect>
          <![endif]-->
       </td>
```

The second step would be to update the styles of your button on the remaining clients, it is as easy as editing your HTML:

``` html
       < a href=”https:sanjoseearthquaketickets.org”
           style=”
               background-color: #938acb;
               border: 1px solid #938383;
               border-radius: 4px;
               color: #dfdfdf;
               display: inline-block;
               font-family: Arial Bold, sans-serif;
               font-size: 20px;
               font-weight: bold;
               line-height: 55px;
               text-align: center;
               width: 270px;
               mso-hide: all; “>
         Buy Tickets</a>
```

One thing to note is that the reason why these styles get hidden from microsoft word is because of the vendor property mso-hide: all.




Some preprocessors add links as a feature:


Let’s say you have a phone number included on your footer, the phone number is in its own table row and table cell just like this:

``` html
       <tr>
        <td align=”center”
            class=”color: #ffffff;
            font-family: Arial, sans-serif;
            font-weight: bold;
            padding: 0 0 30px 0; “>
       For more info call 1650-555-555
        </td>
       </tr>
```

If you would take a look at this code in apple’s preprocessor you would see that the numbers we have added have turned into a link, so now you have a default link in your email that does not match the design you want. You don’t have access to the HTML that created the link but lucky for us apple mail does support CSS in a style tag, so you can use a class to target and style the anchor tag.

Use a span and add a class to target specific links.


 Another encounter i had with the apple rendering engine was recently when i was trying to change the font-size of some of the content on my footer, i was trying to make the text smaller than 14px, unfortunately some clients won’t allow this, apple for instance will render type at a minimum of 14px by default. 14px on a footer could be over-dramatized for the viewing audience, lucky for us there are vendor specific properties that exist to override these defaults, webkit and microsoft allow a text-size adjustment that will make it so your text will render at the specific pixel value that you set. Let me show you how this is done below:

``` html

       <td …..
         style=”....
         font-size: 5px;
         -ms-text-size-adjust: none;
         -webkit-text-size-adjust: none; “>
         2550 San Jose Drive No. 155
       </br>
        Santa Clara Complex
       </br>
        CA 94063
         ………..
```
