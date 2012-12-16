# jquery-traverse

The jquery-traverse plugin will give you a flexible way to traverse through containers and their child elements with either keyboard commands or custom events.

## Requirements

* jQuery 1.4.2+

## Installation

Add the following to your HTML head:

``` html
    <script src="jquery.js" type="text/javascript"></script>
    <script src="jquery.traverse.js" type="text/javascript"></script>
```

## Usage

Basic use case:
``` javascript
    $('.some_table').traverse('tbody tr');
```
This will do the following:

1. Add a class of 'highlight' onto the first found 'tbody tr' element within '.some_table'
2. Let you move up and down between these elements (removing and adding the 'highlight' class) with the j/k keys

Advanced use case:
``` javascript
    $('.some_table').traverse('tbody tr', {
        skip_selector: '.skip',
        loop: false,
        move_scrollbar: false,
        key_action: 18, // alt
        key_down: [74, 40], // j, down arrow
        key_up: [75, 38], // k, up arrow
        on_action_override: function() {
            $('.last_action').text($('.highlight td:first').text());
        }
    });
```
This will do the following:

1. Add a class of 'highlight' onto the first found 'tbody tr' element within '.some_table'
2. Skip over elements with the 'skip' class
3. Not loop (once you hit your last 'tbody tr' element going 'down' once more will not jump back to the first 'tbody tr')
4. Not move the scrollbar to keep the current 'highlight' class visible
5. Fire the 'action' event on 18
6. Fire the key_down event on 74 or 40
7. Fire the key_up event on 75 or 38
8. Execute a custom 'action' method on the 'action' event

## Demos

1. [DIV example][example_1]
2. [TABLE example][example_2]
3. [TABLE example (using more options)][example_3]

... more to come.

## Options

<table style="width: 100%; border: 1px solid #000000; margin-bottom: 25px;" border="1" cellspacing="0" cellpadding="3">
  <tbody>
  <tr>
    <th style="width: 200px; background-color: #6690bc;" align="center" valign="middle">
      <span style="color: #ffffff;">Option Name</span>
    </th>
    <th style="width: 200px; background-color: #6690bc;" align="center" valign="middle">
      <span style="color: #ffffff;">Default</span>
    </th>
    <th style="background-color: #6690bc;" align="center" valign="middle">
      <span style="color: #ffffff;">Purpose</span>
    </th>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>jump_between</em></td>
    <td style="text-align: right; padding-right: 10px;"><em>true</em></td>
    <td style="padding-left: 10px;">whether or not traversal should be made between parent containers</td>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>loop</em></td>
    <td style="text-align: right; padding-right: 10px;"><em>true</em></td>
    <td style="padding-left: 10px;">whether or not traversal should loop around to the beginning/end of the traversal elements</td>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>skip_selector</em></td>
    <td style="text-align: right; padding-right: 10px;"><em></em></td>
    <td style="padding-left: 10px;">the selector(s) to skip over during traversal</td>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>table_row_helper</em></td>
    <td style="text-align: right; padding-right: 10px;"><em>false</em></td>
    <td style="padding-left: 10px;"><div>attempting to account for inconsistent table markup</div>
                                    <div>Specifically, tables with their header row as:</div>
                                    <ul>
                                      <li>the first row in the tbody</li>
                                      <li>the first row in the table with no thead or tbody</li>
                                    </ul>
    </td>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>move_scrollbar</em></td>
    <td style="text-align: right; padding-right: 10px;"><em>true</em></td>
    <td style="padding-left: 10px;">whether or not the scrollbar should be moved to keep the highlighted element visible</td>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>highlight_class</em></td>
    <td style="text-align: right; padding-right: 10px;"><em>"highlight"</em></td>
    <td style="padding-left: 10px;">the class to be added to each traversal element</td>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>action_window_location_href<br></em></td>
    <td style="text-align: right; padding-right: 10px;"><em>true<br></em></td>
    <td style="padding-left: 10px;">whether or not the first anchor found in the highlighted element on the action event should be used to navigate the browser to that href</td>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>action_selector</em></td>
    <td style="text-align: right; padding-right: 10px;"><em>' > td > a'</em></td>
    <td style="padding-left: 10px;">the selector to be used if action_window_location_href is true to navigate the page on the action event</td>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>key_event<br></em></td>
    <td style="text-align: right; padding-right: 10px;"><em>"keydown"<br></em></td>
    <td style="padding-left: 10px;">the jQuery event to listen to for keyboard interaction</td>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>key_action</em></td>
    <td style="text-align: right; padding-right: 10px;"><em>13 (enter key)</em></td>
    <td style="padding-left: 10px;">the keyboard keyCode that will fire the action event (this action can be overridden using the on_action_override option)</td>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>key_down</em></td>
    <td style="text-align: right; padding-right: 10px;"><em>74 (j key)</em></td>
    <td style="padding-left: 10px;">the keyboard keyCode that will fire the down event (this action can be overridden using the on_key_down_override option), which by default will move the highlight class down one matching element</td>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>key_up</em></td>
    <td style="text-align: right; padding-right: 10px;"><em>75 (k key)</em></td>
    <td style="padding-left: 10px;">the keyboard keyCode that will fire the up event (this action can be overridden using the on_key_up_override option), which by default will move the highlight class up one matching element</td>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>key_ignore_when_selector</em></td>
    <td style="text-align: right; padding-right: 10px;"><em>'input:focus, button:focus'</em></td>
    <td style="padding-left: 10px;">the selectors in which the plugin should take no action if any matching elements are found</td>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>on_action_before</em></td>
    <td style="text-align: right; padding-right: 10px;"><em></em></td>
    <td style="padding-left: 10px;">an overrideable function that will fire before the action event is fired</td>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>on_action_after</em></td>
    <td style="text-align: right; padding-right: 10px;"><em></em></td>
    <td style="padding-left: 10px;">an overrideable function that will fire after the action event is fired</td>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>on_action_override</em></td>
    <td style="text-align: right; padding-right: 10px;"><em></em></td>
    <td style="padding-left: 10px;">an overrideable function that will fire instead of the default action event</td>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>on_key_down_before</em></td>
    <td style="text-align: right; padding-right: 10px;"><em></em></td>
    <td style="padding-left: 10px;">an overrideable function that will fire before the key down event is fired</td>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>on_key_down_after</em></td>
    <td style="text-align: right; padding-right: 10px;"><em></em></td>
    <td style="padding-left: 10px;">an overrideable function that will fire after the key down event is fired</td>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>on_key_down_override</em></td>
    <td style="text-align: right; padding-right: 10px;"><em></em></td>
    <td style="padding-left: 10px;">an overrideable function that will fire instead of the default key down event</td>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>on_key_up_before</em></td>
    <td style="text-align: right; padding-right: 10px;"><em></em></td>
    <td style="padding-left: 10px;">an overrideable function that will fire before the key up event is fired</td>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>on_key_up_after</em></td>
    <td style="text-align: right; padding-right: 10px;"><em></em></td>
    <td style="padding-left: 10px;">an overrideable function that will fire after the key up event is fired</td>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>on_key_up_override</em></td>
    <td style="text-align: right; padding-right: 10px;"><em></em></td>
    <td style="padding-left: 10px;">an overrideable function that will fire instead of the default key up event</td>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>jump_between_up_before</em></td>
    <td style="text-align: right; padding-right: 10px;"><em></em></td>
    <td style="padding-left: 10px;">an overrideable function that will fire before the jumping up event is fired</td>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>jump_between_up_after</em></td>
    <td style="text-align: right; padding-right: 10px;"><em></em></td>
    <td style="padding-left: 10px;">an overrideable function that will fire after the jumping up event is fired</td>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>jump_between_up_override</em></td>
    <td style="text-align: right; padding-right: 10px;"><em></em></td>
    <td style="padding-left: 10px;">an overrideable function that will fire instead of the default jumping up event</td>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>jump_between_down_before</em></td>
    <td style="text-align: right; padding-right: 10px;"><em></em></td>
    <td style="padding-left: 10px;">an overrideable function that will fire before the jumping down event is fired</td>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>jump_between_down_after</em></td>
    <td style="text-align: right; padding-right: 10px;"><em></em></td>
    <td style="padding-left: 10px;">an overrideable function that will fire after the jumping down event is fired</td>
  </tr>
  <tr>
    <td style="text-align: right; padding-right: 10px;"><em>jump_between_down_override</em></td>
    <td style="text-align: right; padding-right: 10px;"><em></em></td>
    <td style="padding-left: 10px;">an overrideable function that will fire instead of the default jumping down event</td>
  </tr>
  </tbody>
</table>

That's it! Please note, however, that currently only one usage of the plugin is supported on the page at any given time.

## Contributing to jQuery-traverse

Once you've made your great commits:

1. [Fork][forking] jQuery-traverse
2. Create a feature branch
3. Write your code (and tests please)
4. Push to your branch's origin
5. Create a [Pull Request][pull requests] from your branch
6. That's it!

## Links

* Code: `git clone git://github.com/adelegard/jquery-traverse.git`
* Bugs: <http://github.com/adelegard/jquery-traverse/issues>

## Copyright

Copyright © 2012 Alex Delegard. See LICENSE.txt for
further details.

[forking]: http://help.github.com/forking/
[pull requests]: http://help.github.com/pull-requests/
[example_1]: http://htmlpreview.github.com/?https://github.com/adelegard/jquery-traverse/blob/master/examples/example_1.html
[example_2]: http://htmlpreview.github.com/?https://github.com/adelegard/jquery-traverse/blob/master/examples/example_2.html
[example_3]: http://htmlpreview.github.com/?https://github.com/adelegard/jquery-traverse/blob/master/examples/example_3.html
