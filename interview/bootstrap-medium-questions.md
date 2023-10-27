# Bootstrap Medium Interview Questions

#### 1. What do you know about links and typography in Bootstrap?
  Links are used to make HTML elements clickable whereas Typography is used for formatting and styling the content. Typography is used to create paragraphs, lists, inline elements and many other design-oriented styles of fonts.

#### 2. What are button groups in Bootstrap?
   - Button groups are very useful in the Bootstrap framework that allow developers to stack multiple buttons in a line together. Other than this, they can be used to place the alignment buttons together and optional JavaScript radio.

#### 3. What are Labels and badges in Bootstrap?
   - Bootstrap “.label” is a predefined class that gives more details related to links and text on the web page. This can include warnings, counts, updates, etc. Badges are components that serve to display an indicator or count a number. They are similar to labels except that they have more rounded corners.  

4. What is the Bootstrap page header?
   - The Bootstrap page header is a component that is used to add appropriate spacing between headings on a web page. This feature helps to demarcate the more important headings from the less important ones by adding visual hierarchy to the page. The page header can be customized using CSS to change the font size, color, and other properties of the text. Additionally, the page header can be used to add a background color or image to the header, making it a versatile tool for creating visually appealing and organized layouts in web applications. Overall, the Bootstrap page header is a useful component for creating visually appealing and well-organized web pages.

5. **What do you know about pagination and its types?**
   - Pagination informs about the presence of a series of interrelated contents across numerous pages. They are built using HTML elements with each page hyperlinked to another page.

      There are two types of pagination-active and disabled.

        **`Active pagination:`** This highlights the current page number making it easy for the user to know the page they are currently on. “.active” class is used here.

        **`Disabled state pagination:`** This allows you to disable certain page links using “.disabled” option

6. **List some contextual classes in Bootstrap?**
   - In Bootstrap, contextual classes are used to provide "contextual feedback" for the users. These classes are mostly used with the components like Alerts or Badges to denote the type or category. These contextual classes can be used within a Bootstrap component to add meaning through colors. However, the syntax may vary slightly depending on the component. Bootstrap includes several predefined contextual classes:

        **`.text-primary:`** For light blue colored text

        **`.bg-primary:`** For light blue colored background

        **`.text-secondary:`** For grey colored text

        **`.text-danger:`** For red colored text

        **`.text-warning:`** For orange colored text

        **`.text-decoration-none:`** For removing the text decoration

        **`.text-break:`** For breaking words to prevent overflow        

7. **What is lead body copy in Bootstrap?**
    - The lead body copy in Bootstrap is a component that is used to highlight or emphasize a particular paragraph on a web page. It creates a large font size and adds light fonts or tall length lines to the text, making it stand out from the rest of the content. The lead body copy is commonly used for introductory paragraphs or important messages that need to be highlighted for the user. The lead class can be added to any paragraph element in Bootstrap to create the lead body copy effect. Overall, the lead body copy is a useful tool for creating visually appealing and attention-grabbing content in web applications.        

8. **How can you create a Pills navigation menu in Bootstrap?**
    - Pills are a preferred navigation style as they improve user experience and navigation flow. To create a navigation menu, you will need to include the right Bootstrap classes and know what function those classes perform. So, in order to create a pills navigation menu, add the class .nav-pills to the nav element along with .nav class. Here we use the .nav class as it is the base class for any navigation style in Bootstrap. Here .nav class element wraps .nav-link class element. Also, the .nav-link class should be given to all link elements available in the navbar. 

9. **Differentiate between Bootstrap Grid system and other grid systems?**
    - Bootstrap's grid system is among the most popular web layout systems used by developers, but there are many other grid systems like Foundation, CSS Grid Layout, Flexbox, and so on. Here's how Bootstrap's grid system differs from others:

        **`Bootstrap Grid System:`**
       - Bootstrap uses a 12-column responsive grid system, allowing for different arrangements of content across different screen sizes.
       - It uses a straightforward and consistent class naming convention that includes the screen size, grid behavior, and the number of columns.
       - The Bootstrap grid system uses Flexbox in Bootstrap 4 (and later versions). It replaced the Floats grid system used in Bootstrap 3.
       - It even compensates for padding, margins, and nested rows and columns.
       - As part of a large library, it comes with many additional components and JavaScript plugins.

        **`Foundation Grid System:`**
       - Like Bootstrap, Foundation also uses a 12-column grid system.
        -However, Foundation allows users to customize the grid system (number of columns, breakpoints, etc.) by modifying a settings file.
       - In addition to the basic grid, it includes separate grid layouts for small (mobile), medium (tablet), and large (desktop) screens.
       - It requires slightly more complex class naming and organization, which can be more difficult for beginners.

        **`CSS Grid Layout:`**
       - CSS Grid Layout is a native CSS module, not a library, and offers a two-dimensional grid-based layout system.
      -  CSS Grid provides more control over the layout and placement of elements, regardless of their HTML source order, enabling complex layouts.
       - It defines both rows and columns, unlike Bootstrap's column-based system.
       - It doesn't require additional classes as Bootstrap does. However, using it effectively requires a thorough understanding of CSS.

        **`Flexbox:`**
       - Flexbox is also a native CSS module, designed for one-dimensional layouts.
       - It allows for responsive elements within a container to be automatically arranged based upon screen size.
       - Flexbox is simpler and more flexible than the traditional grid systems but might be less intuitive compared with the grid system in Bootstrap or Foundation.
       - The Bootstrap grid system uses Flexbox in Bootstrap 4 and later, inheriting much of its flexibility and responsiveness.

        In conclusion, different contexts or project requirements may lead developers to favor one grid system over another. Bootstrap's grid is highly intuitive and easy to implement, especially for those already using Bootstrap. In contrast, native CSS modules like CSS Grid and Flexbox allow more control over placement and layout but require a deeper understanding of CSS.       

10. **What can you do to add an image to your web page using Bootstrap?**
    - We can add an image to a webpage using Bootstrap using the built-in img class.

          <img src="abc,jpg" class="img-fluid" alt="Responsive img">

      Here img tag adds the images to the web page, img-fluid makes the image responsive and resizes automatically, the alt attribute provides a description of the image.        

11. **Explain Bootstrap's "container" class?**
    - This class provides a fixed-width container for web page content. It ensures that your content remains within a certain width, irrespective of the screen size. Let’s see this through an example.
    
          <div class="container">
            <!-- here goes your content -->
          </div>


      Here the class container creates a container for your content. And, then the content can be added inside the div element. This class keeps the content centered and with padding on both sides.    

12. **What is the difference between "container" and "container-fluid" classes in Bootstrap?**
    - The main difference between the "container" and "container-fluid" classes in Bootstrap is the width and padding of the container. The "container" class creates a container that has a fixed width and horizontal padding. This means that the content inside the container will be centered and have a maximum width based on the screen size.

        The "container-fluid" class, on the other hand, creates a container that takes up the full width of the view with no horizontal padding. This means that the content inside the container will stretch to fill the entire width of the screen.

        In summary, the "container" class is used to create a fixed-width container with horizontal padding, while the "container-fluid" class is used to create a full-width container with no horizontal padding. The choice of which class to use depends on the design requirements of the web page and the desired layout of the content.        

13. **List some benefits of using Bootstrap?**
    - Bootstrap offers a host of advantages, making it a popular choice among developers for front-end design and development. Here are some of the key benefits:

        **`Responsive Design:`** Bootstrap ensures that your website is automatically adjustable to any screen size and resolution. This makes your website design responsive and mobile-friendly.

        **`Consistency:`** Bootstrap ensures consistency across different platforms, and even among team members. It provides a centralized development code, each element of which has been meticulously curated by the Bootstrap team.

        **`Customizable:`** Developers have flexibility to choose the features that are required, resulting in a lightweight and efficient code. With its Sass variables and mixins, developers can customize the Bootstrap’s components, grid system, typography, colors, button sizes and much more.

        **`Extensive List of Components:`** Bootstrap contains numerous ready-to-use components which can enhance your development process such as navigation bars, dropdown menus, modals, carousels, tooltips, and many more.

        **`Strong Grid System:`** Bootstrap incorporates a powerful 12-column responsive grid system, which assists developers in organizing the layout of pages and makes it easy to create complex and flexible layouts.

        **`Compatibility:`** Bootstrap is compatible with all major browsers like Chrome, Firefox, Internet Explorer, Safari and Opera. Therefore, it ensures that your website or application will render effectively across various browsers.        

14. **Explain Bootstrap's "row" class in the Grid system?**
    - In Bootstrap's Grid system, the .row class serves as a wrapper for columns. It's a key part of the grid system structure, which fundamentally consists of containers, rows and columns.

      Bootstrap row class creates a horizontal row of columns in the grid system. It provides a horizontal layout and makes column using col class in Bootstrap grid system. This class can be used on webpage to make an attractive web application.    

15. **What are Bootstrap's typography classes?**
    - Bootstrap provides a set of typography classes grouped into several categories which allow you to manipulate your text style in terms of headings, alignment, transformation, color, weight, display headings, and more. Such as:

        **`display-1:`** For large, bold heading.

        **`lead:`** For making text stand out.

        **`text-muted:`** To make the text look as less as important.

        **`text-primary:`** Makes text appear in your theme’s primary color.          

16. **How does Bootstrap ensure cross-browser compatibility?**
    - Bootstrap ensures cross-browser compatibility through CSS and JavaScript that work successfully across varied browsers and versions. Besides, it holds browser specific css and Javascript files like HTML5 shim and Respond.js which makes sure that the features of Bootstrap work correctly on all browsers.    

17. **How can you create a responsive layout using Bootstrap?**
    - To create a responsive layout, one can use the grid system in Bootstrap with its responsive classes. The grid system that has rows and columns allow to define width of each column with “col-:” classes. Besides this, some other responsive classes like "col-sm-", "col-md-", "col-lg-", and "col-xl-" can be used to provide different column widths for different screen sizes.

18. **Tell me about Bootstrap's "col" class in the Grid system ?**
    - In the Bootstrap grid system, the .col class is crucial for defining columns within a .row. The grid is a 12-column layout, so all the columns within a row should add up to 12 for full width coverage under a certain size. The columns are responsive, and will automatically adjust their width and position based on the screen size.

       It can be used in combination with other classes such as col-sm, col-md, col-lg, and col-xl to make the size of the columns suitable for different screen sizes.     

19. **What is the use of Bootstrap's "badge" component?**
    - The Bootstrap's badge component is typically used to create small count indicators and labels. Badges can be used to highlight specific items, denote a status, or catch attention with a small identifier. Here are some examples of common uses:

        **`Highlight New or Unread Items:`** A "New" badge can be added to menu items, listings, or graphical elements on a web page to draw attention.

        **`Notification Count or Indicator:`** In navigation bars, badges are often used to indicate the number of unread notifications, messages, or updates.

        **`Status Identifier:`** Changes in status, like "Success", "Danger", "Warning", "Info" can be highlighted using badges with contextual color classes.              

20. **What is the Bootstrap grid system? Give an example?**
    - Bootstrap's grid system is a responsive, mobile-first system that can be scaled up to 12 columns per the increase in device size or viewport size. Predefined classes for easy layout options and powerful mix-ins for generating successful semantic layouts are featured in this system.

                        HTML
                        <div class="container">
                        <div class="row">
                            <div class="col-sm">
                            One of three columns    
                        </div>    
                        <div class="col-sm">
                            One of three columns
                            </div>
                            <div class="col-sm">
                            One of three columns
                            </div>
                        </div>
                        </div>        

21. **What do you mean by page header in Bootstrap?**
    - A page header is used to add spacing around page headings, which can be created using the class .page-header.

22. **Why do we use ‘Jumbotron’ in Bootstrap?**
    - To highlight the web page's content, we use jumbotron in Bootstrap. It provides a margin for the landing page's content and enlarges the heading. You must create a container div with the class .jumbotron to implement it.

23. **What is the affix plugin in Bootstrap?**
    - We are allowed to affix an `<div>` HTML tag to a particular location by affix plugin. We can even turn on and off the pinning by using this plugin, for example- social icons. It will start at one position, but when the web page reaches a specific point, the `<div>` tag will be frozen at a particular place and no longer scroll with the rest of the web page.

24. **Discuss Bootstrap tables and various classes that can change the appearance of the table.**
    - Bootstrap offers convenient tools for building and styling tables on web pages. It delivers different classes that permit you to modify the table's appearance. These classes can change borders, spacing, and color, making designing tables that match your website's style more comfortable.                        

25. **What is ‘normalize’ in Bootstrap?**
    - To ensure whether the content on your web page is consistent or not across different browsers, we use Normalize in Bootstrap. In other words, Bootstrap uses Normalize for establishing cross-browser consistency. It is a modern and HTML5-ready alternative to CSS resets. Better cross-browser consistency is provided by this small CSS file in the default styling of HTML elements.    

26. **What are Glyphicons in Bootstrap? How do we use it?**
    - In our web projects, we can use icon fonts called Glyphicons. Glyphicons halflings require licensing as they are not free. But they are free of cost for Bootstrap projects.You must use the following code anywhere in your project to use the icons. You can leave space between the text and the icon for proper padding.

            HTML
            <span class = "glyphicon glyphicon-man"></span>    

27. **What do you mean by Bootstrap breadcrumb?**
    - For displaying information for a site in the hierarchy, we use Bootstrap breadcrumbs. With a .breadcrump class, it is an unordered list.

      **For example-** in the case of blogs, breadcrumbs can be used to display categories, date of publishing, or tags. Here the separator is automatically added by CSS.            

28. **How can the Nav element be created in Bootstrap?**
    - Bootstrap provides various options for styling navigation elements. Same markup and base class .nav are used by all of them. for creating a tabular navigation bar or tabs, you need to follow the below-given steps-

        - You can start with an unordered list with a base class of .nav
        - Now you can add .nav-tabs class      

29. **What are the types of lists that Bootstrap supports?**
    - There are three types of lists supported by Bootstrap-

        - **`Ordered List`**

        Sequential order is followed by this type of list and is prefaced by numbers.
        
        - **`Unordered List`**

        This type of list doesn't have any particular order and is styled with bullets. If you don't want the bullets, then by using the class .list-unstyled, you can remove the styling.
        
        - **`Definition List`**

        `<dt>` and `<dd>` elements can be used to define each list item in this type of list. `<dt>` stands for definition term and `<dd>` is the definition of `<dt>` (definition term).        

30. **How do you make images responsive?**
    - A class called .img-responsive to an "a" tag to make it responsive for users. Other way is to add .img-fluid class to `<img>` HTML tag to make image responsive. It applies .max-width:100%, styles and height : auto.         

31. **How can we draw a toolbar of buttons in Bootstrap?**
    - Unique sets of button groups are combined by the class .btn-toolbar to create more complex components.

32. **What is a button group in Bootstrap?**
    - When you want to stack multiple buttons on a single line together, we use button groups. Also, when you want to place items in a group, like alignment buttons together.We use .btn-group class for building a basic button group if we use the .btn type with the .btn-group class to wrap a series of buttons.

33. **How can Bootstrap be used for making thumbnails?** 
    - You need to follow the below-given steps for creating a thumbnail using Bootstrap-

        - With the class of **`.thumbnail,`** add `<a>.` the tag around an image.
        - It will help to add four pixels of padding and a gray border.
        - Now while hovering on to the image, an animated glow will outline the image.    

34. **What is the use of the carousel plugin in Bootstrap?**
    - We use the carousels plugin in Bootstrap: 

       To make sliders on the website pages. 
    
       To display large contents within a small space by adding a slider.
 
       **`Examples:`**

        **`.carousel(‘options’)`**

        With optional options object, a carousel is initialized and starts cycling through items.

        **`.carousel(‘next’)`**

        This type of carousel cycles to the next item. In other words, it is a slideshow for cycling through a series of information/content.

        **`.carousel(‘cycle’)`**

        This type of carousel cycles through the items of carouse from left to right.

        **`.carousel(‘pause’)`**

        This type of carousel stops the carousel from cycling through the carousel items.

        **`.carousel(‘prev’)`**

        This type of carousel cycles to the previous item.

        **`.carousel(‘number’)`**

        This cycles the carousel to a particular frame.

        **`.carousel('dispose')`**

        This one destroys a carousel of an element.      

35. **What are responsive utility classes in Bootstrap?**
    - For concealing or exhibiting the HTML elements, which are based on screen resolution and discerned by a media query, we use a set of classes called Responsive utility.

       **Example-**  “hidden-md-down”      

36. **Is there any relationship between Bootstrap and JavaScript?**

    - Yes, there is a relationship between the two technologies. Some Bootstrap components require JavaScript to work properly.

      **Some of the components that require JavaScript are shown in the below list:**
        - Alerts – To close alerts
        - Buttons – To toggle buttons
        - Checkbox – For checkbox functionality
        - Radio button – For radio button functionality
        - Carousels – For sliding behaviour of carousels
        - Dropdowns – For displaying and positioning dropdowns
        - Modals – For displaying, positioning, and scrolling modals
        - Navbar – To extend collapse plugin to implement responsive behaviour
        - Toasts – For displaying and dismissing toasts
        - Tooltips – For displaying and positioning tooltips
        - Popovers – For displaying and positioning popovers
        - Scrollspy – For scrolling behaviour and navigation updates

37. **What are the different options for adding Bootstrap to your project?**
    - There are several options to add Bootstrap to your project.

       **They are:**
        - Using ready-to-use compiled CSS and JS code.
        - Using source files.
        - Installing via Bootstrap CDN.
        - Installing via package managers such as NPM, Yarn, RubyGems, Composer, etc.

38. **Can we learn Bootstrap without learning CSS?**
    - The simple answer is no. We cannot learn it without learning CSS as it is a CSS framework. Therefore, knowledge of CSS is essential to understand the basic concepts of Bootstrap.                   

39. **What is the function of the transition plugin in Bootstrap?** 
    - It provides simple transition effects like sliding or fading in modals.

40. **Explain the concept of creating a basic form in Bootstrap?**
    - First, add a `<form>` element. Then, inside the form element, wrap labels and controls in a `<div>` element with the .form-group class. Next, the .form-control class to text input elements like <`input>, <textarea>` and `<select>` elements.

41. **What is a scrollspy in Bootstrap?**
    - It is an auto-updating nav component that allows in fetching section of the page based on the scroll position. The .active class will update accordingly from one nav item to another based on the scroll position.

42. **What is the function of the affix plugin in Bootstrap 3?**
    - Affix is a jQuery plugin. It allows `<div>` element to be attached to a location on the page.

      **Example:** Use of the social icon on a page. The icons will start in a location, but when the page hits on a certain mark, it will block the `<div>` element in place and will stop the scrolling for the rest of the page.

43. **What is the purpose of the grid system?**
    - By using the grid system, we can make up to 12 columns across a page. Different classes have been defined for this purpose.  

44. **What is well in Bootstrap 3?**
    - Bootstrap well is a form of container which thrives or makes the content look recessed on the web page. It also wraps the content using the .well class.      

45. **What will be the output of the below code and why?**

            <div class="progress">
                    <div class="progress-bar bg-success" style="width: 65%">
                            <span class="sr-only">75% successfully completed</span>
                    </div>
                    <div class="progress-bar bg-warning" style="width: 20%">
                            <span class="sr-only">30% completed with warnings</span>
                    </div>
                    <div class="progress-bar bg-danger" style="width: 15%">
                            <span class="sr-only">15% did not complete</span>
                        </div>
            </div>
     - If we place multiple bars with the same .progress parent element, Bootstrap will pile them into one single progress bar. As we know, in Bootstrap the sum of the progress bar is 100%. So, the progress bar will give the result full width and fully populated.    

46. **How can we customize links to pagination?**
    - We can customize the links by using the .disabled class for unclickable links and the .active class for indicating the current page.

47. Explain input groups in Bootstrap4.
    - Input group is put out from controls.

      We can prepend and append addons elements to a .form-control in front of or behind text inputs by using the .input-group-prepend class and the .input-group-append class respectively. Further, you can use the .input-group-sm class to make a small input group and the .input-group-lg class to make a large input group.    

48. **Explain what Bootstrap’s collapsing elements is?**
    - It allows you to collapse any particular element without using any JavaScript code.

      To use this feature in Bootstrap, you have to add data-toggle=” collapse” to the controller element along with a data target to automatically assign the control of a collapsible element. We can use this by writing .collapse(options) etc.

49. **Define Bootstrap 4 thumbnails?**
     - It is a way to use the layout images, videos, text, etc. in a grid system. We can create thumbnails by adding a tag with the .img-thumbnail class around the image.

50. **Explain the modal in Bootstrap4?**
    - A model is an inherited window that is layered over its parent window. This is used to augment the user experience and add different functionalities. Model windows are created with the help of the modal plugin.             

