#### 1. What is Bootstrap ?
   `Bootstrap` is a platform for web development based on a front-end framework. It is used to create exceptional responsive designs using `HTML`, and `CSS`. These templates are used for forms, tables, buttons, typography, models, tables, navigation, carousels and images. Bootstrap also has Javascript plugins, which are optional. Bootstrap is mostly preferred for developing mobile web applications.

#### 2. Explain why Bootstrap is preferred for website development ?
   Bootstrap has better features as compared to other web development platforms. It provides extensive browser support for almost every known browser such as Opera, Chrome, Firefox, Safari, etc. If you are well-acquainted with CSS and HTML, web development becomes easy on Bootstrap.
    Also, it supports mobile applications with the help of responsive design and can adjust CSS as per the device, screen size, etc. Instead of creating multiple files, it creates only a single file reducing the work of a developer.   

#### 3. What are the key components of Bootstrap?
   The key components of Bootstrap include:
      **`CSS`**: It consists of  various CSS files
      **`Scaffolding:`** It provides a basic structure with the Grid system, link styles, and background
      **`Layout Components:`** This gives the list of layout components
      **`JavaScript Plugins:`** It contains many `jQuery` and JavaScript plugins
      **`Customize:`** To get your own version of the framework, you can customize your components    

#### 4. List some features of Bootstrap?
   Some of the features of Bootstrap are:
        It provides an open-source for use
        Bootstrap has Compatibility with all browsers
        It has Responsive designs
        Easy to use and fast       

#### 5. What are Class loaders in Bootstrap?
   A class loader is a part of JRE or Java Runtime Environment which loads Java classes into Java virtual environment. Class loaders also perform the process of converting a named class into its equivalent binary form.

#### 6. How many types of layout are available in Bootstrap?
   - There are two major layouts for Bootstrap:
        - **`Fluid Layout-`** This layout is necessary for creating an app that is 100 % wider and covers all the screen width.
        - **`Fixed Layout-`** It is used only for a standard screen (940px). Both layouts can be used for creating a responsive design.            

#### 7. What is Bootstrap Grid System?
   Bootstrap includes a responsive, mobile-first fluid grid system that appropriately scales up to 12 columns as the device or viewport size increases. It includes predefined classes for easy layout options, as well as powerful mixins for generating more semantic layouts.

#### 8. Give an example of a basic grid structure in Bootstrap ?
   Example of a basic grid structure:
        <div class = "container">
            <div class = "row">
            <div class = "col-*-*"></div>
            <div class = "col-*-*"></div>
            </div>        
            <div class = "row">...</div>
        </div>           

#### 9. Why do we use Jumbotron in Bootstrap ?
   Jumbotron is used for highlighting content in bootstrap. It could either be a slogan or probably a headline. It increases the heading size and gives a margin for the content of the landing page. To implement Jumbotron in a Bootstrap, you have to use:
        Create a container `<div>` with the class of .jumbotron
        For example, use `<div class=”container”>` if you don’t want Jumbotron to reach the screen’s edge.                    


#### 10. What are the two codes used for code display in Bootstrap?
   - There are two simple ways to display code in Bootstrap:
        - **`<code> tag:`** This tag is used to display an inline code.
        - **`<pre> tag:`** If you have a code with several lines or even a block element, you can display it using this.        

#### 11. Explain the typography and links in Bootstrap?
   - Bootstrap sets a basic global display (background), typography, and link styles.
      - **`Basic Global display`** − It sets background-color: #fff; on the <body> element.
      - **`Typography`** − This uses the @font-family-base, @font-size-base, and @line-height-base attributes as the typographic base
      - **`Link styles −`** It sets the global link color via attribute @link-color and applies link underlines only on :hover.        

#### 12. What is a progress bar in bootstrap?
   Progress bar is used with HTML tag style in HTML element using `<progress>` keyword. In bootstrap we use html5 `<progress>` with CSS classes that have special features in bootstrap, that is only made for the progress bar.

#### 13. How do you make images responsive?
   Bootstrap allows to make the images responsive by adding a class .img-responsive to the `<img>` tag. This class applies max-width: 100%; and height: auto; to the image so that it scales nicely to the parent element.    

#### 14. What are the steps for creating basic or vertical forms?
   - The steps for creating basic or vertical forms include:
        - Add a role form to the parent `<form>` element
        - Wrap labels and controls in a `<div>` with class .     form-group.This is required to achieve optimum spacing
        - Add a class of .form-control to all texturl `<input>` , `<textarea>` , and `<select>` elements.

#### 15. What is Bootstrap collapsing elements?
   Bootstrap collapsing elements enable you to collapse any particular element without writing any JavaScript code or the accordion markup. To apply collapsing elements in bootstrap, you need to add data-toggle= “collapse” to the controller element along with a data-target or href to automatically assign control of a collapsible element. Also, you can use .collapse (options), .collapse (‘show’) or .collapse (‘hide’) for the same.               

#### 16. Explain types of lists supported by Bootstrap ?
   Bootstrap supports three types of lists such as:
        **`Ordered lists −`** An ordered list is a list that falls in some sort of sequential order and is prefaced by numbers.
        **`Unordered lists −`** An unordered list is a list that doesn’t have any particular order and is traditionally styled with bullets. If you do not want the bullets to appear then you can remove the styling by using the class .list-unstyled.
        **`Definition lists −`** In this type of list, each list item can consist of both the `<dt>` and the `<dd>` elements. `<dt>` stands for definition term. Subsequently, the `<dd>` is the definition of the `<dt>`    

#### 17. What is media object in Bootstrap and what are their types?
   Media objects in Bootstrap help you to put media object like image, video or audio to the left or right of the content blocks. Media element can be created using the class .media and the source is specified in using the class .media-object. Media-objects are of two types.
    The two types of media object are:
        **.media**
        **.media-list** 

#### 18. Explain the uses of carousel plugin in Bootstrap ?
   Carousel plugin in bootstrap is used to make sliders in the web pages or your site. There are several carousel plugins that are used in bootstrap to display large contents within a small space by adding sliders.
       **`Examples:`** .carousel(options), .carousel(‘pause’), .carousel(cycle’), .carousel(‘prev’), .carousel(‘next’).               

#### 19. How can you create Nav elements in Bootstrap?
   Bootstrap offers various options for styling navigation elements. All of these use the same markup and base class .nav. You need to perform the following steps to create Tabular Navigation or Tabs:
        Start with a basic unordered list with the base class of .nav
        Add class .nav-tabs    

#### 20. What are glyphicons? How to use them?
   Glyphicons are icon fonts which can be used in your web projects. Glyphicons Halflings are not free and require licensing. However, their creator has made them available for Bootstrap projects without any cost.
      To use the icons, you just have to use the following code just about anywhere in your code. Leave a space between the icon and text for proper padding.
          <span class = "glyphicon glyphicon-search"></span>

#### 21. What are the steps to create basic or vertical forms?
   The steps involved in creating vertical or basic forms are:
        Firstly, a role form can be added to the parent `<form>` element.
        Next, you have to add appropriate spacing by wrapping labels and control in `<div>` and using the function ‘class .form-group’.
        Finally, apply the function ‘class .form-control’ to different elements such as text url `<input>` , `<textarea>` and `<select>`           

#### 22. What do you mean by Bootstrap well?
   Bootstrap well is nothing but a container that makes the content appear sunken. Sometimes it may also give an inset effect on the webpage. Thus, a developer can create a well and also wrap the content in the well with the help of `<div>` and class .well. The content would appear as per your wish.

#### 23. What are the input groups in Bootstrap?
   Input groups are extended Form Controls. You can easily prepend and append text or buttons to the text-based inputs with the help of input groups. Also, you can add common elements to the user’s input. For example, you can add the dollar symbol, the @ for a Twitter username, or anything else that might be common for your application interface.
      To prepend or append elements to a .form-control you need to do the following:
        Wrap it in a `<div>` with class .input-group
        In the next step, place your extra content inside a `<span>` with class .input-group-addon.
        Now place this `<span>` either before or after the `<input>` element.   

#### 24. What is Bootstrap breadcrumb?
   - Breadcrumbs are a great way to show hierarchy-based information for a site. In the case of blogs, breadcrumbs can show the dates of publishing, categories, or tags. They indicate the current page’s location within a navigational hierarchy.
    A breadcrumb in Bootstrap is simply an unordered list with a class of .breadcrumb. The separator is automatically added by CSS.     

#### 25. How to create thumbnails using Bootstrap?
   To create thumbnails using Bootstrap you need to do the following:
        Add an `<a>` tag with the class of .thumbnail around an image.
        It will add four pixels of padding and a gray border.
        Now, on hover, an animated glow will outline the image.    

#### 26. What is a Bootstrap Container?
   A bootstrap container is a class which is useful and creates a central area within the page where our site content can be put within. The advantage of the bootstrap .container is that it is responsive and will place all our other HTML code.            

#### 27. What is pagination in bootstrap and how are they classified?
   Pagination is the handling of an unordered list by bootstrap. If you want to handle pagination, bootstrap provides the following classes:
        **`.pagination:`** To get pagination on your page you have to add this class
        **`.disabled, .active:`** Customize links by .disabled for unclickable links and .active to indicate the current page
        **`.pagination-Ig, .pagination-sm:`** Use these classes to get different size item.

#### 28. What are bootstrap alerts and how will you create them?
   Bootstrap Alerts provide a way to style messages to the user. They provide contextual feedback messages for typical user actions. You can add an optional close icon to alert. Also, you can add a basic alert by creating a wrapper `<div>` and adding a class of .alert and one of the four contextual classes.     

#### 29. How will you create a Bootstrap Dismissal Alert?
   You need to follow a few steps to build a dismissal alert:
        First, you have to add a basic alert by creating a wrapper  `<div>` and adding a class of .alert and one of the four contextual classes.
        Also add optional .alert-dismissable to the above `<div>`class.
        Next, you have to add a close button.
        Finally, use the `<button>` element with the data-dismiss = “alert” data attribute. 

#### 30. What are the steps to create a progress bar using bootstrap?
   To create a basic progress bar, you need to do the following:
        Add a `<div>` with a class of .progress.
        Next, inside the above `<div>`, add an empty `<div>` with a class of **`.progress-bar`**.
        Add a style attribute with the width expressed as a **`percentage`**. For example, style = “40%”; indicates that the progress bar was at 40%.    

#### 31. What are the bootstrap media objects?
   The media objects are abstract object styles for building various types of components like blog comments, Tweets, etc. It features a left-aligned or right-aligned image alongside the textual content. The goal of the media object is to make the code for developing these blocks of information drastically shorter. And, this goal is achieved by applying classes to some of the simple markups.   
          
#### 32.What are the steps to create an animated progress bar using bootstrap?
   The steps to create an animated progress bar are as follows:
        Add a `<div>` with a class of .progress and .progress-striped. Also add class .active to .progress-striped.
        Next, inside the above `<div>`, add an empty `<div>` with a class of .progress-bar.
        Add a style attribute with the width expressed as a percentage. For example, style = “60%”; indicates that the progress bar was at 60%.     

#### 33. What do you mean by column ordering in Bootstrap?
   Column ordering is one of the most interesting features found in bootstrap. By using appropriate functions, the columns can be written easily and also in a defined order. You can also show them in another column. In order to change or alter the order of the column easily, the functions **.col-md-push-*** and **.col-md-pull-8*** can be used.             

#### 34. What is the Bootstrap Grid System?
   The Bootstrap Grid System is a responsive, mobile-first system that scales up to 12 columns as per the increase in the device or viewport size. The system features predefined classes for easy layout options and powerful **mix-ins** for generating effectively semantic layouts. 

#### 35. What Are Bootstrap Media Queries?
   Media Queries in Bootstrap allow you to move, show and hide content based on viewport size.  Here is an example to show the basic structure of Bootstrap grid:
                <div class = "container">
                    <div class = "row">
                    <div class = "col-*-*"></div>
                    <div class = "col-*-*"></div>
                    </div>     
                    <div class = "row">...</div>
                </div>      

#### 36. What is Normalize in Bootstrap?
   Bootstrap uses Normalize to establish cross-browser consistency.
       Normalize.css is a modern, HTML5-ready alternative to CSS resets. It is a small CSS file that provides better cross-browser consistency in the default styling of HTML elements.                 

#### 37. What are Bootstrap panels? Explain how to create a Bootstrap panel with a heading ?
   Bootstrap panel components are used for putting your DOM component in a box. To get a basic panel, simply add .panel and .panel-default classes to the `<div>` element. There are two ways of adding panel heading to a Bootstrap panel:
        Use any of the `<h1>, <h2>, <h3>, <h4>, <h5>`, or `<h6>` tags with a .panel-title class
        You can also use the .panel-heading class  

#### 38. What is the purpose of using the Scrollspy plugin?
   The purpose of using the **`Scrollspy plugin`** in Bootstrap is that it allows you to target certain sections of the page based on the scroll position. Thereafter, you can add .active classes, based on the scroll position, to the Bootstrap navbar.             

#### 39. Why do we use the affix plugin in Bootstrap?
   We use the affix plugin in Bootstrap for affixing a `<div>` to some certain location on a webpage. The plugin also allows toggling pinning on and off for the affixed `<div>`. Social icons are the most popular example of using the affix plugin in Bootstrap.
       The affixed `<div>` starts from a particular location on the webpage and scrolls with it. However, after a certain mark, it will be locked in place, thus stopping scrolling with the rest of the webpage.    

#### 40. What is the Bootstrap Panel?
   When there is a need for putting the contents in a bordered box with some padding around, the panel components are used. They can be created with the .panel class and content inside the panel consists of a .panel-body class. For creating a basic panel, you need to add class .panel to the `<div>` element and add class .panel-default to this element.

#### 41. What is Button group and which class is used for basic button group?
   Button groups allow multiple buttons to be stacked together on a single line. You can use this when you want to place items like alignment buttons together.
      For basic button group, **`.btn-group`** class is used. Here, you can wrap a series of buttons with class .btn in .btn-group.

#### 42.What will be the default Bootstrap look of the alert created with this following code?            
   <div class="alert" role="alert">Warning! I'm missing something.</div>
    Alert messages are used to provide feedback message and they usually require the attention of the user. Here it is important to note that Bootstrap Alerts don’t have default class. If a contextual class such as .alert-success, .alert-info, .alert-warning, or .alert-danger, is not provided, a default gray alert will be created.   

#### 43. Why do we need to use Bootstrap?
   Bootstrap provides major benefits to a developer. Some of them include:
        It is a **`free`** and **`open-source`** Web Designing Framework.
        Bootstrap has the support of all the **`web browsers`** like Internet Explorer, Google Chrome, Firefox, Opera, Safari, etc.
        It is a very powerful mobile first **`front-end`** framework.
        Also, it is very easy to start as one needs to have an idea of **`HTML`** and **`CSS`** only to work with it.
        We can design a **`responsive website`** through it which adjust to desktop, tablet, and mobile.
        It comprises functional **`built-in components`** which are easy to customize.       

#### 44. Explain Glyphicons in Bootstrap 3? 
   Glyphicons are reusable components that provide beautiful icons (these icons are known as glyphs) under a wide range of categories. It can almost use anywhere in your code. Glyphicons do not only provide icons or glyphs, they also provide support for dropdowns, input groups, navigation, alerts, etc.
          <span class=”glyphicon glyphicon-search”></span>
      **Note:** Bootstrap 4 does not support Glyphicons. Therefore, you can use the following icon sets when dealing with v4.
        - Font Awesome
        - Iconic
        - Octicons

#### 45. What is the function of the transition plugin in Bootstrap?
   It provides simple transition effects like sliding or fading in modals.        

#### 46. Explain the function of the following code segment?
  <a href="#">Home <span class="badge badge-primary">36</span></a>
    This code will produce a link with an inline badge which will give an important notification to the user like number received, messages received, or the number of requests, etc. Further, the **`.badge-primary`** class will add a blue color to the badge.

#### 47. What is a toast and what are the main components of a toast?
   It is like an alert box that appears for a small time. The main components of a toast are the toast header and the toast body.    

#### 48. What will be the output of the below code?
   <div class="row">
            <div class="col-6 col-md-4">A</div>
            <div class="col-6 col-md-4">B</div>
            <div class="col-6 col-md-4">C</div>
   </div>
    According to the above code segment, the columns start at 50% of width on mobile devices and reduce up to 33.3% of width on desktop devices.

#### 49. What are the dependencies required to work Bootstrap properly?
   jQuery is the only dependency required to work Bootstrap properly. 

#### 50. What are the global styles that are used in Bootstrap 4 default typography?
   These are as follows:
        **Font family –** Native font stack
        **Font size –** Default root font size of the browser that is usually 16px
        **Line height –** 1.5
