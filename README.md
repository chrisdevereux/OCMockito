![mockito](http://docs.mockito.googlecode.com/hg/latest/org/mockito/logo.jpg)

OCMockito enables mocks creation, verification and stubbing.


Mac and iOS
===========

OCMockito is supported for both Mac and iOS development.

__Mac:__

Add OCHamcrest.framework and OCMockito.framework and to your project.

Add a Copy Files build phase to copy both OCHamcrest.framework and
OCMockito.framework and to your Products Directory. For unit test bundles, make
sure this Copy Files phase comes before the Run Script phase that executes
tests.

Add:

    #define HC_SHORTHAND
    #import <OCHamcrest/OCHamcrest.h>

    #define MOCKITO_SHORTHAND
    #import <OCMockito/OCMockito.h>

Note: If your Console shows

    otest[57510:203] *** NSTask: Task create for path '...' failed: 22, "Invalid argument".  Terminating temporary process.

double-check your Copy Files phase.

__iOS:__

Add OCHamcrestIOS.framework and OCMockitoIOS.framework to your project.

Add "-lstdc++" and "-ObjC" to your "Other Linker Flags".

Add:

    #define HC_SHORTHAND
    #import <OCHamcrestIOS/OCHamcrestIOS.h>

    #define MOCKITO_SHORTHAND
    #import <OCMockitoIOS/OCMockitoIOS.h>


Let's verify some behavior!
===========================

    // mock creation
    NSMutableArray *mockArray =  mock([NSMutableArray class]);

    // using mock object
    [mockArray addObject:@"one"];
    [mockArray removeAllObjects];

    // verification
    [verify(mockArray) addObject:@"one"];
    [verify(mockArray) removeAllObjects];

Once created, the mock will remember all interactions. Then you can selectively
verify whatever interactions you are interested in.


How about some stubbing?
========================

    // mock creation
    NSArray *mockArray =  mock([NSArray class]);

    // stubbing
    [given([mockArray objectAtIndex:0]) willReturn:@"first"];

    // following prints "(null)" because objectAtIndex:999 was not stubbed
    NSLog(@"%@", [mockArray objectAtIndex:999]);


Argument matchers
=================

OCMockito verifies argument values by testing for equality. But when extra
flexibility is required, you can specify OCHamcrest matchers.