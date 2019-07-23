# ASP.NET MVC Live Project - Front End Focus
## Table of Contents
  <a href="#intro">Introduction</a>

  <a href="#app1">Application 1 - Erector's Inc</a>  
* <a href="#nav1">Nav Bar Upgrades</a>
* <a href="#links">Link Styling and Animation</a>

<a href="#app2">Application 2 - Management Portal</a>  
* <a href="#chat">Chat Box Modal</a>
* <a href="#datepicker">Date Picker Pop Up</a>
* <a href="#nav2">Collapsible Nav Bar</a>
* <a href="#tables">Table Styling</a>
* <a href="#news">Company News Re-Work</a>

<a href="summary">Sprint Summary</a>  

## <span id="intro">Introduction to the Project</span>
During my training at the Tech Academy, I joined a team of peers on a two week development sprint. There were two projects I worked on during the sprint. Both ASP.NET MVC web applications using Entity Framework. The first application was nearing a minimal viable product for the client, and the other application was starting from ground zero. My primary focus during the sprint was to complete front end user stories, though some back end coding was also involved. This is my code retrospective for the sprint, which includes the user stories I worked on, and what I learned through the process. 

## <span id="app1">Application 1 - Erector's Inc</span>
The client hired us to make an employee management portal for their construction company. The application kept track of employee status, company news, job site information, and scheduling. The application mostly needed cosmetic touch ups because it was nearly the minimal viable product. I started by resolving some nav bar styling conflicts, then moved on to adding link animations and ensuring buttons across the site had a uniform appearance. 

### <span id="nav1">Nav Bar Upgrades</span>
My first challenge was identifying the cause of inconsistent behavior with the current nav bar. After searching through the code base, I discovered overlapping JavaScript functions that were causing opacity issues and link hover effects to display incorrectly. To resolve the issues, I consolidated the functions and tested to ensure the effects were behaving as expected. 

The next user story I completed was adding animation effects to the nav bar. I chose a gradient underline that expands to fill the link's background when the mouse focuses on it. The menu dropdowns turn the same lighter background color and change to blue when hovered. 

I also tweaked the opacity of the nav bar so while it's covering the header image, the background has .8 opacity. Scrolling beyond the image, the nav bar transitions to full opacity and adds a border to stand out from the main body content. Some Bootstrap classes needed to be overwritten in order for the effects to function properly. Here is a snip of the CSS, along with a picture of the overall effect.
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

To be thorough, I used CSS media rules so the nav bar background color and transitions looked good on mobile as well.

![Mobile nav bar](https://github.com/jrs-scott/Front-End-Code-Retrospective/blob/master/mobileNavbar.JPG)

### <span id="links">Link Styling and Animation</span>
The sub navigation links across the site were inconsistently placed and had no styling. To improve user experience, I ensured the links were in the same spot on every page. Using the same color scheme as the rest of the site, I then styled the links into buttons that raise up and display a small shadow when the mouse hovers over them.
![Button styling](https://github.com/jrs-scott/Front-End-Code-Retrospective/blob/master/buttonStyling.JPG)

## <span id="app2">Application 2 - Management Portal</span>
After finishing my tickets on the Erector's Inc application, I transferred to the management portal project. My team was the first to break code on the application, which was really exciting. Since everything was new, there was some shuffling around and multiple changes were made to accommodate the growth of new features. 

### <span id="chat">Chat Box Modal</span>
One of my assigned user stories was to create a pop up chat box that worked across the application. To implement this feature, I used a Bootstrap modal and some good old fashioned CSS. The modal's HTML: 

``` html
<div id="chat-modal" class="modal modal-right" tabindex="-1" role="dialog" aria-hidden="true">
    <div class="modal-dialog" role="document">
        <div class="modal-content">
            <div id="chat-header" class="modal-header">
                <button type="button" class="close" data-dismiss="modal" aria-label="Close" onclick="closeChat()" data-backdrop="true">
                    <span aria-hidden="true"><i id="close-icon" class="glyphicon glyphicon-remove"></i></span>
                </button>
                <h3 class="modal-title text-center">Welcome to Chat!</h3>
            </div>
            <form class="modal-body">
                <ul id="discussion"> 
                    <li><strong>Bob Smith</strong>: Hello everyone, quick reminder about the upcoming meeting tomorrow.</li>
                    <li><strong>Jane Doe</strong>: It starts at 9:00am.</li>
                </ul>
                <textarea id="message-box" placeholder="Type a message here..." required></textarea>
                <button id="send-message" type="button" class="btn btn-info">Send</button>
            </form>
        </div>
    </div>
</div>
```

This is the resulting chat container. Functionality was later added using SignalR, so the text was simply for an example.
![Chat box](https://github.com/jrs-scott/Front-End-Code-Retrospective/blob/master/chatModal.JPG)

### <span id="datepicker">Date Picker Pop Up</span>
The application had a multitude of forms with inconsistent date pickers. I implemented a jQuery plugin and applied it to each form instance that required date selection so they would be uniform accross the site. 

The CSHTML code:
```html
@Html.LabelFor(model => model.DateStamp, htmlAttributes: new { @class = "control-label col-md-2" })
<div class="col-md-10">
	@Html.EditorFor(model => model.DateStamp, new { htmlAttributes = new { @class = "form-control date-picker", autocomplete = "off" } })
	@Html.ValidationMessageFor(model => model.DateStamp, "", new { @class = "text-danger" })
</div>
```
The simple script required:
``` JavaScript
$(function () {
    $(".date-picker").datepicker();
});
```
And finally, an image of what it looks like in action:
![Date picker](https://github.com/jrs-scott/Front-End-Code-Retrospective/blob/master/datepicker.JPG)

### <span id="nav2">Collapsible Nav Bar</span>
Another user story I completed was to build a vertical navigation bar that could collapse down to icons. This took a fair amount of research with trial and error. Multiple changes were made to the nav bar as time went on, so I don't have the final code snip or an image of the icon toggling, but here is an image during progress to get an idea of how it turned out. Each link ended up with an icon, and there were arrows added that would point left or right depending on the state of the nav bar. With a click, it would expand or collapse to show only the column of icons.

![Vertical nav bar](https://github.com/jrs-scott/Front-End-Code-Retrospective/blob/master/verticalNavbar.jpg)

### <span id="tables">Table Styling</span>
A feature of the application included managing shift times for employees. The data was displayed with no styling as black text over an image so you couldn't even read the information. I used Bootstrap and Fontawesome to create a table that stood out against the background and included icons to quickly identify links. 

The CSHTML code uses a foreach loop to go through the data and present it in the table.
```HTML
								<h2>Shift Times</h2>

<p>
    <a type="button" class="btn btn-sm btn-primary" href="@Url.Action("Create")">
        <i class="fa fa-plus-square"></i> Create New
    </a>
</p>
<table class="table table-striped table-bg table-hover">
    <tr>
        <th scope="col">
            @Html.DisplayNameFor(model => model.Monday)
        </th>
...
    </tr>

    @foreach (var item in Model) {
        <tr scope="row">
            <td>
                @Html.DisplayFor(modelItem => item.Monday)
            </td>
...
            <td class="text-right">
                <a type="button" class="btn btn-sm btn-primary" href="@Url.Action("Edit", new { id = item.ShiftTimeId })">
                    <span>
                        <i class="fa fa-pencil"></i> Edit
                    </span>
                </a>
                <a type="button" class="btn btn-sm btn-primary" href="@Url.Action("Details", new { id = item.ShiftTimeId })">
                    <span>
                        <i class="fa fa-list"></i> Details
                    </span>
                </a>
                <a type="button" class="btn btn-sm btn-primary" href="@Url.Action("Delete", new { id = item.ShiftTimeId })">
                    <span>
                        <i class="fa fa-trash"></i> Delete
                    </span>
                </a>
            </td>
        </tr>
    }

</table>
```
And here is the result:
![Shift time table](https://github.com/jrs-scott/Front-End-Code-Retrospective/blob/master/tableStyling.JPG)


### <span id="news">Company News Re-Work</span>
Part of what I worked on was a database restructure. The project manager wanted the models to change from using a Guid to an int ID primary key. There were other changes made through the application to ensure the data was congruent, but here are some small code snips.

The company news model field I added:
``` C#
        [Key]
        [DatabaseGenerated(DatabaseGeneratedOption.Identity)]
        public int NewsId { get; set; }
```
The updated controller method for editing news:
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

It was a great experience to work on applications that were in two entirely different stages of their development life cycles. During the sprint I had the opportunity to do the follow, which I am confident will benefit my career in the future. 
* Problem solve bugs and find solutions for them
* Work within deadlines to complete user stories
* Gain additional C# experience in the scope of an MVC project
* Collaborate with a team of peers
* Contribute to daily stand ups and weekly code retrospectives
* Research new ways to implement navigation bars
* Use JavaScript to alter HTML properties and utilize on click events

