[![Build Status](https://travis-ci.org/rvdkooy/reflux-store-status.svg?branch=master)](https://travis-ci.org/rvdkooy/reflux-store-status)

# reflux-store-status
A reflux store mixin that makes your store status aware.


With [reflux](https://github.com/reflux/refluxjs) js you can create async actions that you typically use for API calls. By using this mixin you can easily give your users feedback during those calls based on the status of your store.

```
// In your store:
var store = Reflux.createStore({
    mixins: [StoreStatusMixin],
    onLoadData: function() {
        this.pending(); // this puts the store status into PENDING and triggers
    },  
    onLoadDataCompleted: function(data) {
        this._state = data;
        this.ready(); // this puts the store status into READY and triggers
    }
});

// In your component:
var Component = React.createClass({
    render: function() {

        if(this.state.status === store.statusCodes.PENDING) {
            
            // show progress indicator
        } else if (this.state.status === store.statusCodes.READY) {

            // show the things from the store
        } else {
            
            // do something else
        }
    }
});

```

The store can contain the following status codes:
- INITIAL
- PENDING
- READY
- FAILED

The following Store helpers are available:
```
// to put the store into the READY status:
this.ready();
this.ready(newstate); // puts the store into the READY status and updates the state

// to put the store into the PENDING status:
this.pending(newstate);

// to put the store into the FAILED status:
this.failed(newstate);

// to put the store into any or your own status:
this.setStatus(status);

// to reset the store into the INITIAL status
this.resetToInitialStatus();

```
Note: Only the ready, pending and failed helpers accept an optional parameter which will be used to update the state!
