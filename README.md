# Web-Crawler

## Web Crawler Notebook flow
 
 In this notebook initially a set of seed urls were provided, which were then put in a frontier (comprised of front and back queues). Then each thread out of set of 9 pops a url
 one of the back queue present in the frontier. After poping the url from one of the back queue the same thread checks if that queue gets empty, if so then it populates it with 
 further urls until it doesn't remain empty. After populating the queue with some url, the thread then hits the Url using urlib library with the help of http request response
 protocol. After the hitting and fetching the content of hit url. The content is parsed using BeautifulSoup library and further urls are extracted from the content. These
 extracted set of urls are then passed through a set of different modules. Firstly these set of extracted modules are passed through a filteration module, where it is checked
 whether every specific url from the set of extracted urls are allowerd to being hit or accessed, it is done on the basis of robot.txt file of every url specified domain, this 
 file tells that against a particular domain are allowed to hit or not. After this set if filtered urls are passed through a duplicate url elimination module, where it is checked
 that whether every filtered url is previously crawled or not, if it is already being previously crawled then it is removed from the list. After passing through the duplicate
 elimination module, the reamining set of urls are added in to the frontier so that in the next iteration any particular thread can pop them out of back queue and crawl them. This
 whole life cycle continues until a certain threshold (indicating specific no of urls are being crawled) ia reached.
 
## Url Frontier Structure

 Url frontier is composed of two different type of queues i.e front queues and back queus. The number of front queues and back queues for now are kept 5 and 3 respectively. As  
 first step some urls from set of seed urls are pushed to these front queues. The assigning of urls to these front queues are done on the basis of priority number. For producing 
 priority against every url "prioritizer" function is implemented which takes a url and returns a number as priority of that url, the range of that priority number is in between 1 
 and no of front queues. Next mapping is done in such way that if priority no is 1 then that specified url will be assigned the front queue 1 and similarly if the priority no is 2
 then that url will be assigned to front queue 2 and so on.
 
 Next for moving the urls from front queus to back queues logic is implemented in such a way that there lies a greater chance of urls with greater priority to be selected to go to 
 the back queues as compared to those with lower priority. Another important point here is that only the url with same domain can come in back queues for example if the back queue 
 1 has one url with Oracle.com domain then next url that comes in this back queus will also be of Oracle.com domain. Yes if any back queue gets empty only then the domain of this 
 back queue can be changed and you can move any url with other domain from front queue to back queue. In additon to all this, the url from front queue can only come to the back 
 queue only if that back queue is empty otherwise not. Futhermore a time stamp is kept with every back queue, indicating the earliest possible time any url from that back queue 
 can popped out and taken by thread. This is done to avoid frequent request access to same domain websit. The thread takes (Pops) the url from that back queue whose time stamp is 
 smaller than or equal to current time and shortest among all other back queues, this indicates that you can access this url earliest and also as its time stamp is shorter than or 
 equal to current time so you can access it. Once a url is taken out from any back queue the 15 seconds are added to the time stamp of that back queue so that same domain url will 
 be accessed atleast 15 seconds later next time.
 
 ## What to Install
As this is a simply python notebook file so you just have to install Annaconda environment along with jupyter notebook. You can install the both of these by following the youtube vedio link provided as below.

https://youtu.be/5mDYijMfSzs
 
