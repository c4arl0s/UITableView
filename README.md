# Creating and Managing Table Views

# iOS Tables

# Delegation

# Creating Tables

## Table Styles

# Laying Out the View

- UITableView class descends from UIScrollView class.

## Asigning a Data Source

- The table's dataSource property sets an object to act as a table's source of cells.

# Serving Cells

NSIndexPath class, describe the path through a data tree to a particular node

``` objective-c
NSIndexPath *indexPath = [NSIndexPath indexPathForRow:5 inSection:0];
```

# Registering Cell Class by Class

```objective-c
[self.tableView registerClass:[UITableViewCell class] forCellReuseIdentifier:@"table cell"];
```

# Registering Cell Class by XIBs (iOS 5 and later)

``` objective-c
[self.tableView registerNib: [UINib nibWithNibName:@"CustomCell"] bundle:[NSBundle mainBundle]] forCellReuseIdentifier:@"custom cell"];
```
# Dequeueing Cells

# Asigning a delegate

- if you are working directly with a UITableView, assign the delegate property to a responsible object.

# Recipe: Immplementing a Basic table

# Data Source Methods

- numberOfSectionsInTableView
- tableView:numberOfRowsInSection:
- tableView:cellForRowAtIndexPath:

# Woow, all the code written in one .m file WOOW, All credits by Erica Sadun

``` objective-c
/*
 
 Erica Sadun, http://ericasadun.com
 iOS 7 Cookbook
 Use at your own risk. Do no harm.
 
 */

@import UIKit;
@import QuartzCore;
#import "Utility.h"


#pragma mark - TestBedViewController

@interface TestBedViewController : UITableViewController
@end

@implementation TestBedViewController
{
    UIFont *imageFont;
    NSArray *items;
}

// Number of sections
- (NSInteger)numberOfSectionsInTableView:(UITableView *)aTableView
{
	return 1;
}

// Rows per section
- (NSInteger)tableView:(UITableView *)aTableView numberOfRowsInSection:(NSInteger)section
{
    return items.count;
}

// Return a cell for the index path
- (UITableViewCell *)tableView:(UITableView *)aTableView cellForRowAtIndexPath:(NSIndexPath *)indexPath
{
	UITableViewCell *cell = [self.tableView dequeueReusableCellWithIdentifier:@"cell" forIndexPath:indexPath];
    // Cell label
    cell.textLabel.text = [items objectAtIndex:indexPath.row];
    
    // Cell image
    NSString *indexString = [NSString stringWithFormat:@"%02d", indexPath.row];
    cell.imageView.image = stringImage(indexString, imageFont, 6.0f);
	return cell;
}

// On selection, update the title and enable find/deselect
- (void)tableView:(UITableView *)aTableView didSelectRowAtIndexPath:(NSIndexPath *)indexPath
{
    UITableViewCell *cell = [self.tableView cellForRowAtIndexPath:indexPath];
    self.title = cell.textLabel.text;
    self.navigationItem.rightBarButtonItem.enabled = YES;
    self.navigationItem.leftBarButtonItem.enabled = YES;
}

// Deselect any current selection
- (void)deselect
{
    NSArray *paths = [self.tableView indexPathsForSelectedRows];
    if (!paths.count) return;
    
    NSIndexPath *path = paths[0];
    [self.tableView deselectRowAtIndexPath:path animated:YES];
    self.navigationItem.rightBarButtonItem.enabled = NO;
    self.navigationItem.leftBarButtonItem.enabled = NO;
    
    self.title = nil;
}

// Move to the selection
- (void)find
{
    [self.tableView scrollToNearestSelectedRowAtScrollPosition:UITableViewScrollPositionTop animated:YES];
}


// Set up table
- (void)viewDidLoad
{
    [super viewDidLoad];
    self.view.backgroundColor = [UIColor whiteColor];
    
    self.navigationItem.rightBarButtonItem = BARBUTTON(@"Deselect", @selector(deselect));
    self.navigationItem.leftBarButtonItem = BARBUTTON(@"Find", @selector(find));
    self.navigationItem.rightBarButtonItem.enabled = NO;
    self.navigationItem.leftBarButtonItem.enabled = NO;
    
    imageFont = [UIFont fontWithName:@"Futura" size:18.0f];
    [self.tableView registerClass:[UITableViewCell class] forCellReuseIdentifier:@"cell"];
    items = [@"Alpha Bravo Charlie Delta Echo Foxtrot Golf Hotel India Juliet Kilo Lima Mike November Oscar Papa Romeo Quebec Sierra Tango Uniform Victor Whiskey Xray Yankee Zulu" componentsSeparatedByString:@" "];
}

@end


#pragma mark - Application Setup

@interface TestBedAppDelegate : NSObject <UIApplicationDelegate>
@property (nonatomic, strong) UIWindow *window;
@end

@implementation TestBedAppDelegate

- (BOOL)application:(UIApplication *)application didFinishLaunchingWithOptions:(NSDictionary *)launchOptions
{
    _window = [[UIWindow alloc] initWithFrame:[[UIScreen mainScreen] bounds]];
    _window.tintColor = COOKBOOK_PURPLE_COLOR;
    TestBedViewController *testBedViewController = [[TestBedViewController alloc] init];
    testBedViewController.edgesForExtendedLayout = UIRectEdgeNone;
    UINavigationController *navigationController = [[UINavigationController alloc] initWithRootViewController:testBedViewController];
    _window.rootViewController = navigationController;
    [_window makeKeyAndVisible];
    return YES;
}

@end


#pragma mark - main

int main(int argc, char *argv[])
{
    @autoreleasepool
    {
        int retVal = UIApplicationMain(argc, argv, nil, @"TestBedAppDelegate");
        return retVal;
    }
}
```




