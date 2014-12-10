timeout-dialog.js
=================

Timeout-dialog.js is a JQuery plugin that displays a timeout popover after a certain period of time. The timeout dialog should be used whenever you want to display to the user that the logged in session is about to expire. It creates a light box with a countdown and options to stay signed in or sign out.

Example and Documentation
-------------------------

[timeout-dialog.js examples](http://rigoneri.github.com/timeout-dialog.js)


Credit
------

timeout-dialog.js was developed by [@rigoneri]

Usage
-----

In a Rails application, setup a route:

    get 'prevent_timeout' => 'sessions#prevent_timeout'

In the corresponding `prevent_timeout` action in `SessionsController`, reset the variable being used for the timeout counter. For example, with [Sorcery](https://github.com/NoamB/sorcery) and the `session_timeout` submodule, you could do something like this:

    def prevent_timeout
      session[:last_action_time] = Time.now.in_time_zone if current_user
      render nothing: true
    end

Finally, plug this in at the end of your `application.html.haml` but still inside the html tag:

    - if current_user
      :javascript
        $.timeoutDialog();

Good as gold!
