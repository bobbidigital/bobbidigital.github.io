---
layout: post
status: publish
published: true
title: Structuring Selenium Test Code
author: Jeff
author_login: admin
author_email: jeff@allthingsdork.com
author_url: http://www.allthingsdork.com
wordpress_id: 802
wordpress_url: http://www.allthingsdork.com/?p=802
date: '2013-08-03 16:44:30 -0500'
date_gmt: '2013-08-03 22:44:30 -0500'
categories:
- Tech
- linkedin
tags:
- python
- programming
- testing
- selenium
comments: []
---
<p>I had the opportunity to use the <a href="http://docs.seleniumhq.org">Selenium browser automation</a> suite for a project at my, now previous, job. Our testing needs weren't anything spectacular, especially considering we had absolutely zero in the way of automated testing for the project I was working on. I figured anything now would just be icing on the cake.</p></p>
<p>Playing around with Selenium, the very first thing I struggled with was how to structure my test code. I did a bit of research and a bit of my own architecture to produce a solution that worked well for me. Your mileage may vary.</p></p>
<h2>Page Objects</h2></p>
<p>The first major revelation for me was the idea of structuring each web page as an object. Each of these page objects should return another page object during an operation. Sometimes it might be the same page, other times it will be the resulting page of a particular action. This allows you to handle the <a href="http://docs.seleniumhq.org/projects/webdriver/">WebDriver API</a> inside the Page classes and removes the need of handling drivers in your actual test code.</p></p>
<p><strong>Sample Login Page in Python</strong></p></p>
<pre><code>class LoginPage(object):</p>
<p>    def__init__(self, driver=None):<br />
        self.url = '<login url>'<br />
        self.driver = driver or webdriver.Chrome()<br />
        self.driver.get(self.url)</p>
<p>    def type_username(self, username):<br />
        self.driver.find_element_by_id('txtUserName').send_keys(username)<br />
        return self</p>
<p>    def type_password(self, password):<br />
        self.driver.find_element_by_id('txtPassword').send_keys(password)<br />
        return self</p>
<p>    def submit_login(self):<br />
        self.driver.find_element_by_id('btnlogin').click()<br />
        return HomePage(self.driver)</p>
<p>def main():<br />
    loginpage = LoginPage()<br />
    loginpage.type_username('jeff')<br />
    loginpage.type_password('password')<br />
    newpage = loginpage.submit_login()<br />
</code></pre></p>
<p>This quick set of code kind of illustrates the structure of the code. From the client perspective, it masks all of the nasty element searching and driver passing and makes the actual test code (the main routine) pretty clean and legible. Since a lot of testers aren't full blooded programmers, the ease of reading the main routine is probably going to be very appreciated.</p></p>
<h2>Composite Objects and Inheritance</h2></p>
<p>In most situations, a page has several common components. For example, on this blog, every page will have a navigation bar at the top, with menu items. The way I handled this scenario is by making the Navigation bar a composite object of the page. So the navigation is handled by this NavBarComponent. So in my example, I navigate menus by passing a list object that has the name of the navigation tree. So if the menu navigation would be Server->Inventory->Details, I'd pass a list of ['Server', 'Inventory', 'Details'].</p></p>
<pre><code>class NavBarComponent:</p>
<p>    def navigate_menu(self, driver, *args):<br />
        for arg in enumerate(args):<br />
            hover = None<br />
            element = driver.find_element_by_partial_link_text(arg[1])<br />
            hover = ActionChains(driver).move_to_element(element)<br />
            hover.perform()<br />
        click = ActionChains(driver).click(element)<br />
        click.perform()<br />
        page_class = self.get_final_page_object(arg[1])<br />
        return page_class(driver)<br />
</code></pre></p>
<p>The get_final_page_object method is just a method that I created so that I can dynamically return a Page Object. That's not important however for our discussion here. So now, navigation can be handled by this subclass.</p></p>
<pre><code>class HomePage(object):</p>
<p>    def __init__(self, driver):<br />
        self.navbar = NavBarComponent()<br />
        self.driver = driver</p>
<p>    def navigate_menu(self, *args):<br />
        return self.navbar.navigate_menu(self.driver, *args)<br />
</code></pre></p>
<p>Now we have our HomePage object expose the navigate_menu method but simply passes that call to its composite NavBarComponent object. This allowed me to keep my code pretty focused on specific tasks. It also has the added benefit of being able to either update the NavBarComponent independently in the event it's ever changed or we can substitute the NavBarComponent for some specialty Navigation Bar in the event a page behaves differently than others.</p></p>
<p>I extended this same approach to things like DataGrids. Typically a DataGrid object will be reused from page to page. Sure simple things like column names may change, but just by parameterizing those small changes, you can easily use the Datagrid Object across multiple pages.</p></p>
<h3>Inheritance</h3></p>
<p>Lastly, we use inheritance to eliminate more code. In my project, we had a Server Inventory page, a Storage Inventory Page and a Network Device Inventory page. But all these pages had most of the same components and logic. That allowed me to place all the common actions into an InventoryPage class, which handled the nitty gritty things like, sorting by column name or grouping by column name. These are functional steps that would exist on each page. So by encapsulating all of those items into the InventoryPage base class, I can quickly add functionality to a bunch of different pages at once.</p></p>
<p>Here's a quick UML diagram of what this might look like.</p></p>
<p><img src="http://www.allthingsdork.com/images/inventoryuml.png" alt="UML Diagram of InventoryPages" /></p></p>
<p>This is by no means the absolute best way to do things. I'm sure there are plenty with more experience in Selenium that have other approaches. But this approach has been easy to maintain, easy to follow and easy to understand. I think that's what most of us are looking for in our Test Suites. Your mileage may vary.</p></p>
