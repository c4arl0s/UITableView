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



