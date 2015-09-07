
# JASMINE FEEDREADER PROJECT


The test suites describe the RSS feeds, the menu and the feed entries


## Describing RSS feeds

 
    describe('RSS Feeds', function() {
        /* This is our first test - it tests to make sure that the
         * allFeeds variable has been defined and that it is not
         * empty. Experiment with this before you get started on
         * the rest of this project. What happens when you change
         * allFeeds in app.js to be an empty array and refresh the
         * page?
         */

All RSS feeds should:


Be defined and have a length that is not zero

 
        it('should be defined', function() {
            expect(allFeeds).toBeDefined();
            expect(allFeeds.length).not.toBe(0);
        });

Have a url that is defined and not ‘ ‘

 
         it('should have a url', function(){
           for(var i = 0; i < allFeeds.length; i++) {
             expect(allFeeds[i].url).toBeDefined();
             expect(allFeeds[i].url).not.toBe('');
           }
         });

Have a name that is defined and not ‘ ‘

 
         it('should have a name', function(){
           for(var i = 0; i < allFeeds.length; i++) {
             expect(allFeeds[i].name).toBeDefined();
             expect(allFeeds[i].name).not.toBe('');
           }
         });

    });

## Describing the menu

 
    describe('The menu', function() {

The menu should be hidden on default and toggle visibility when the icon is clicked

 
       it('should be hidden by default', function() {
         expect($('body').hasClass('menu-hidden')).toBeTruthy();
       });

        it('should display when the icon is clicked and hide when icon is clicked again', function() {

          $('body').addClass('menu-hidden');
          $('.menu-icon-link').click();
          expect($('body').hasClass('menu-hidden')).toBeFalsy();

          $('body').removeClass('menu-hidden');
          $('.menu-icon-link').click();
          expect($('body').hasClass('menu-hidden')).toBeTruthy();
        });
      });

## Describing initial feed entries

 
    describe('Initial Entries', function() {

Load the feed before each test

 
         beforeEach(function(done){
          loadFeed(0,done);
        });

The feed should have at least one entry

 
        it('should have at least one entry', function(done){
          expect($('.feed').children().length).toBeGreaterThan(0);
          done();
        });
      });

## Describing New Feed Selection

 
    describe('New Feed Selection', function() {

The initial feed results should not be the same as the new feed results.


Feed results from before calling loadFeed() Define initialFeed results as the results loaded before the test is run.

 
      var initialFeed;

Feed results returned after calling loadFeed() Define newFeed results as the results loaded when loadFeed is called again.

 
      var newFeed;

         beforeEach(function(done){
          loadFeed(1, function(){

Set initialFeed equal to the html returned by the loadFeed function before the test is run

 
            initialFeed = $('.feed').html();
            done();
          });
        });

         it('should change content when a new feed is loaded', function(done) {

Check that the loadFeed() function returns results that are different than the initial feed results

 
           loadFeed(0, function() {

Set newFeed equal to the html returned by the loadFeed function

 
             newFeed = $('.feed').html();
           });
           expect(newFeed).not.toBe(initialFeed);
           done();
         })

      });


});