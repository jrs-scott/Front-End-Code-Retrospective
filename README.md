# ASP.NET MVC Live Project - Front End Focus
## Table of Contents
  <a href="#intro">Introduction to the Applications</a>

  <a href="app1">Application 1 - Erector's Inc</a>  
* <a href="nav1">Nav Bar Upgrades</a>
* <a href="links">Link Styling and Animation</a>

<a href="app2">Application 2 - Management Portal</a>  
* <a href="#chat">Chat Box Modal</a>
* <a href="datepicker">Date Picker Pop Up</a>
* <a href="nav2">Collapsible Nav Bar</a>
* <a href="tables">Table Styling</a>
* <a href="news">Company News Re-Work</a>

<a href="summary">Sprint Summary</a>  

## <span id="intro">Introduction to the Project</span>
This is my code retrospective for the two week sprint I joined through the Tech Academy. There were two similar projects I worked on during the sprint: both were ASP.NET MVC web applications using Entity Framework. My primary focus during the sprint was to complete front end user stories, though back end was also involved in a few stories. It was a great experience to work on applications that were in two entirely different stages: one was nearing a minimal viable product for the client, and the other application was starting from ground zero.

## <span id="app1">Application 1 - Erector's Inc</span>
Nearing completion, this application mostly needed cosmetic touch ups. I started by resolving some nav bar styling conflicts, then moved on to adding link animations and ensuring buttons across the site had a uniform appearance. 

### <span id="nav1">Nav Bar Upgrades</span>
The first challenge was to identify what was causing inconsistent behavior with the nav bar. After searching through the app, I discovered overlapping JavaScript causing opacity issues and link hover effects to display incorrectly. Once I resolved that, I added animation effects to the nav bar. A gradient underline expands to fill the link's background when the mouse focuses on it. The menu dropdowns turn the same lighter background color and change to blue when hovered. While the nav bar is covering the header image, the background has .8 opacity. Scrolling beyond the image, it transitions to full opacity and adds a border to stand out from the main body content. Some Bootstrap needed to be overwritten in order for the effects to function properly. Here is a snip of the CSS, along with a picture of the overall effect.
``` css
.underline-animation {
    text-transform: uppercase;
    background-image: linear-gradient(0deg, #A79885 0%, #4E6172 100%);
    background-repeat: no-repeat;
    background-size: 60% 0.2em;
    background-position: 50% 75%;
    transition: background-size 0.25s ease-in;
}

.underline-animation:hover,
.navbar-default .navbar-nav > .open > a,
.navbar-default .navbar-nav > .open > a:hover,
.navbar-default .navbar-nav > .open > a:focus {
    background-color: inherit;
    background-size: 100% 100%;
```

![Nav bar animation](https://github.com/jrs-scott/Front-End-Code-Retrospective/blob/master/horizontalNavbar.jpg)

To be thorough, I also adjusted the nav bar so both the background color and transitions looked good on mobile as well using media rules in the site's CSS.
![Mobile nav bar](https://github.com/jrs-scott/Front-End-Code-Retrospective/blob/master/mobileNavbar.JPG)

### <span id="links">Link Styling and Animation</span>
The general navigation links across the site were inconsistently placed and had no styling. To improve user experience, I ensured the links were in the same spot on every page. Using the same color scheme as the rest of the site, I turned the links into buttons that raise up and display a small shadow when the mouse hovers over them.
![Button styling](https://github.com/jrs-scott/Front-End-Code-Retrospective/blob/master/buttonStyling.JPG)

## <span id="app2">Application 2 - Management Portal</span>
After finishing my user stories on the Erector's Inc application, I transferred to the management portal project. My team was the first to break code on the application, which was really exciting. Since everything was new, there was some shuffling around and multiple changes were made to accomodate the growth of new features. 

### <span id="chat">Chat Box Modal</span>
One of primary user stories was to create a pop up chat box that worked across the application. To implement this feature, I used a Bootstrap modal and some good old fashioned CSS. The modal's HTML: 

``` html

```


![Chat box](https://github.com/jrs-scott/Front-End-Code-Retrospective/blob/master/chatModal.JPG)

### <span id="datepicker">Date Picker Pop Up</span>



### <span id="nav2">Collapsible Nav Bar</span>


### <span id="tables">Table Styling</span>

### <span id="news">Company News Re-Work</span>

``` C#
        [Key]
        [DatabaseGenerated(DatabaseGeneratedOption.Identity)]
        public int NewsId { get; set; }
```

``` C#
        [HttpPost]
        [ValidateAntiForgeryToken]
        public ActionResult Edit([Bind(Include = "NewsId,DateStamp,Title,NewsItem,ExpirationDate")] CompanyNews companyNews)
        {
            if (ModelState.IsValid)
            {
                db.Entry(companyNews).State = EntityState.Modified;
                db.SaveChanges();
                return RedirectToAction("Index");
            }
            return View(companyNews);
        }
```


## <span id="summary">Sprint Summary</span>
