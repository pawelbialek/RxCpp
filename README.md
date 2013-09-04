# Reactive Extensions for C++ (RxCpp)

Reactive Extensions (Rx) is a library for composing asynchronous and event-based programs using observable sequences and LINQ-style query operators.

Data sequences can take many forms, such as a stream of data from a file or web service, web services requests, system notifications, or a series of events such as user input.

Reactive Extensions represents all these data sequences as observable sequences. An application can subscribe to these observable sequences to receive asynchronous notifications as new data arrives. The Rx library is available for application development in C++, .NET, Ruby, Python, Silverlight, Windows Phone 7 and JavaScript. For more information on these different platforms, see Differences Between Versions of Rx topic.

## Pulling vs. Pushing Data

In interactive programming, the application actively polls a data source for more information by pulling data from a sequence that represents the source. The iterator allows us to get the current item by returning the current property, and determines whether there are more items to iterate (by calling some on_next method).

The application is active in the data retrieval process, controlling the pace of the retrieval by calling on_next at its own convenience. This pattern is synchronous, which means that the application might be blocked while polling the data source. Such pulling pattern is similar to visiting your library and checking out a book. After you are done with the book, you pay another visit to check out another one.

On the other hand, in reactive programming, the application is offered more information by subscribing to a data stream (called observable sequence in Rx), and any update is handed to it from the source. The application is passive in the data retrieval process: apart from subscribing to the observable source, it does not actively poll the source, but merely reacts to the data being pushed to it. When the stream has no more data to offer, or when it errs, the source will send a notice to the subscriber. In this way, the application will not be blocked by waiting for the source to update.

This is the push pattern employed by Reactive Extensions. It is similar to joining a book club in which you register your interest in a particular genre, and books that match your interest are automatically sent to you as they are published. You do not need to stand in line to acquire something that you want. Employing a push pattern is helpful in many scenarios, especially in a UI-heavy environment in which the UI thread cannot be blocked while the application is waiting for some events. In summary, by using Rx, you can make your application more responsive.

The push model implemented by Rx is represented by the observable pattern of Rx.Observable/Observer. The Rx.Observable will notify all the observers automatically of any state changes. To register an interest through a subscription, you use the subscribe method of Rx.Observable, which takes on an Observer and returns a disposable. This gives you the ability to track and dispose of the subscription. In addition, Rxs LINQ implementation over observable sequences allows developers to compose complex event processing queries over push-based sequences such as events, APM-based (AsyncResult) computations, Task-based computations, and asynchronous workflows. For more information on the Observable/Observer classes, see Exploring The Major Classes in Rx. For tutorials on using the different features in Rx, see Using Rx.

This section describes in general what Reactive Extensions (Rx) is, and how it can benefit programmers who are creating asynchronous applications.

### In This Section

1\. When Will You Use Rx
2\. Installing Rx
3\. Differences Between Versions of Rx

### Related Sections

Using Rx
Reactive Extensions on MSDN Developer Center

This topic describes the advantage of using Rx for users who are currently using the .NET event model for asynchronous programming.

## Advantages of using Rx

Whether you are authoring a traditional desktop or web-based application, you have to deal with asynchronous programming from time to time. Desktop applications have I/O or UI threads that might take a long time to complete and potentially block all other active threads. However, a user of the modern asynchronous programming model has to manage exceptions and cancellation of events manually. To compose or filter events, he has to write custom code that is hard to decipher and maintain.

In addition, if your application interacts with multiple sources of data, the conventional way to manage all of these interactions is to implement separate methods as event handlers for each of these data streams. For example, as soon as a user types a character, a keydown event is pushed to your keydown event handler method. Inside this keydown event handler, you have to provide code to react to this event, or to coordinate between all of the different data streams and process this data into a useable form.

Using Rx, you can represent multiple asynchronous data streams (that come from diverse sources, e.g., stock quote, tweets, computer events, web service requests, etc.), and subscribe to the event stream using the Observer class. The Observable class maintains a list of dependent Observer threads and notifies them automatically of any state changes. You can query observable sequences using standard LINQ query operators implemented by the Rx.Observable type. Thus you can filter, aggregate, and compose on multiple events easily by using these LINQ operators. Cancellation and exceptions can also be handled gracefully by using extension methods provided by Rx.

The following example shows how easy it is to implement an observable in C++.

      //Declare an observable<br />
      auto values1 = rxcpp::Range(1, 10);<br />
          rxcpp::from(values1)<br />
             .for_each(<br />
                  [](int p) {<br />
                      cout << p << endl;<br />
                  });

You can also use schedulers to control when the subscription starts, and when notifications are pushed to subscribers. For more information on this, see Using Schedulers for Concurrency Control.

## Filtering

One drawback of the C++ event model is that your event handler is always called every time an event is raised, and events arrive exactly as they were sent out by the source. To filter out events that you are not interested in, or transform data before your handler is called, you have to add custom filter logic to your handler.

Take an application that detects mouse-down as an example. In the current event programming model, the application can react to the event raised by displaying a message. In Rx, such mouse-down events are treated as a stream of information about clicks. Whenever you click the mouse, information (e.g., cursor position) about this click appears in a stream, ready to be processed. In this paradigm, events (or event streams) are very similar to lists or other collections. This means that we can use techniques for working with collections to process events. For example, you can filter out those clicks that appear outside a specific area, and only display a message when the user clicks inside an area. Or you can wait a specific period of time, and inform the user the number of valid clicks during this period. Similarly, you can capture a stream of stock ticks and only respond to those ticks that have changed for a specific range during a particular time window. All these can be done easily by using LINQ-query style operators provided by Rx.

In this way, a function can take an event, process it, and then pass out the processed stream to an application. This gives you flexibility that is not available in the current programming model. Moreover, as Rx is performing all the plumbing work at the background for filtering, synchronizing, and transforming the data, your handler can just react to the data it receives and do something with it. This results in cleaner code that is easier to read and maintain. For more information on filtering, see Querying Observable Collections using LINQ Operators.

## Manipulating Events

Rx represents events as a collection of objects: e.g., a OnMouseMove event contains a collection of Point values. Due to the first-class object nature of observables, they can be passed around as function parameters and returns, or stored in a variable.

This topic describes where you can download the Reactive Extensions (Rx) SDK.

## To download Rx

Reactive Extensions is available for different platforms such as C++, Javascript, .NET Framework 3.5, 4.0, 4.5, Silverlight 3 and 4, as well as Windows Phone 7 &amp; 8\. You can download the libraries, as well as learn about their prerequisites at the [Rx MSDN Developer Center.][1]

The following topic describes the various platforms for which you can develop solutions using Reactive Extensions.

To get the latest release of Rx, as well as learn about its prerequisites, please visit the [Rx MSDN Developer Center][1].

## C++

The Reactive Extensions for C++ (RxCpp) is a library for composing asynchronous and event-based programs using observable sequences and LINQ-style query operators in C++.

## Javascript

Rx for Javascript (RxJS) allows you to use LINQ operators in JavaScript. It provides easy-to-use conversions from existing DOM, XmlHttpRequest (AJAX), and jQuery events to push-based observable collections, allowing users to seamlessly integrate Rx into their existing JavaScript-based websites.

RxJS brings similar capabilities to client script and integrates with jQuery events (Rx.Observable.FromJQueryEvent). It also supports Script#.

## Ruby

Rx for Ruby (Rx.rb) allows you to use Linq operators to create push-based observable collections in Ruby.

## Python

RX for Python (Rx.py) allows you to use Linq operators in Python. Rx.py allows you to implement push-based observable collections, allowing users to seamlessly integrate Rx into their existing Python applications.

## .NET Framework

The core Rx interfaces, IObservable and IObserver, ship as part of .NET Framework 4. If you are running on .NET Framework 3.5 SP1, or if you want to take advantage of the LINQ operators implemented in Observable type, as well as many other features such as schedulers, you can download the Rx header-only library in the [Rx MSDN Developer Center][1].

## Silverlight

Silverlight disallows you from making cross-threading calls, thus you cannot use a background thread to update the UI. Instead of writing verbose code using the Dispatcher.BeginInvoke call to explicitly execute code on the main UI thread, you can use the factory Observable.Start method provided by the Rx header-only library to invoke an action asynchronously. Cross-threading is taken care of transparently by Rx under the hood.

You can also use the various Observable operator overloads that take in a Scheduler, and specify the System.Reactive.Concurrency.DispatcherScheduler to be used.

## Windows Phone

Windows Phone 7 ships with a version of the Reactive Extensions baked into the ROM of the device. For more information, see [Reactive Extensions for .NET Overview for Windows Phone][2]. Documentation for this version of the Reactive Extensions can be found in Windows Phone API library at [Microsoft.Phone.Reactive Namespace][3].

The [Rx MSDN Developer Center][1] also contains an updated version of Rx for WP7, which has new definitions in the System.Reactive.Linq namespace. Note that the new APIs will not clash with the library built in to the phone (nor do they replace the version in the ROM). For more information on the differences of these 2 versions, see this [Rx team blog post][4].

Rx is available for Windows Phone 8 as well as Windows Phone 7. A .NET portable library is available using Nuget that is useful for developing libraries that work on Windows Phone, Windows Store apps, and in classic Windows desktop or server applications.

This section includes topics that explain how you use Rx to create and subscribe to sequences, bridge existing events and existing asynchronous patterns, as well as using schedulers. It also describes more advanced tasks such as implementing your own operators.

### In This Section

1. Exploring The Major Interfaces in Rx
2. Creating and Querying Event Streams
3. Subjects
6. Implementing your own operators for IObservable
7. Using Observable Providers

This topic describes the major Reactive Extensions (Rx) interfaces used to represent observable sequences and subscribe to them.

## Observable/Observer

Rx exposes asynchronous and event-based data sources as push-based, observable sequences. This Observable class represents a data source that can be observed, meaning that it can send data to anyone who is interested. It maintains a list of dependent Observer implementations representing such interested listeners, and notifies them automatically of any state changes.

As described in What is Rx, the other half of the push model is represented by the Observer class, which represents an observer who registers an interest through a subscription. Items are subsequently handed to the observer from the observable sequence to which it subscribes.

In order to receive notifications from an observable collection, you use the subscribe method of Observable to hand it an Observer object. In return for this observer, the subscribe method returns a disposable object that acts as a handle for the subscription. This allows you to clean up the subscription after you are done. Calling dispose on this object detaches the observer from the source so that notifications are no longer delivered. As you can infer, in Rx you do not need to explicitly unsubscribe from an event.

Observers support three publication events, reflected by the interfaces methods. OnNext can be called zero or more times, when the observable data source has data available. For example, an observable data source used for mouse move events can send out a Point object every time the mouse has moved. The other two methods are used to indicate completion or errors.

The following lists the Observable/Observer definitions.

      namespace rxcpp {
         template
         struct Observer
         {
            virtual void OnNext(const T&amp;) {};
            virtual void OnCompleted() {};
            virtual void OnError(const std::exception_ptr&amp;) {};

            virtual ~Observer() {}
         };
         
         template
         struct Observable
         {
            virtual Disposable Subscribe(std::shared_ptr&gt; observer) = 0;
            virtual ~Observable() {}
         };
      }

Note that the OnError event returns an exception_ptr type. The example above shows passing the error to a handler function.

You can treat the observable sequence (such as a sequence of mouse-over events) as if it were a normal collection. Thus you can write LINQ queries over the collection to do things like filtering, grouping, composing, etc. To make observable sequences more useful, the Rx header-only library provides many factory LINQ operators so that you do not need to implement any of these on your own. This will be covered in the Querying Observable Collections using LINQ Operators topic.

### See Also

Creating and Subscribing to Simple Observable Sequences Querying Observable Collections using LINQ Operators

This section describes how you can create and subscribe to an observable sequence, convert an existing C++ event into a sequence and query it.

### In This Section

Creating and Subscribing to Simple Observable Sequences
Querying Observable Collections using LINQ Operators

You do not need to implement the Observable interface manually to create an observable sequences. Similarly, you do not need to implement Observer either to subscribe to a sequence. By installing the Reactive Extension header-only library, you can take advantage of the Observable type which provides many LINQ operators for you to create a simple sequence with zero, one or more elements. In addition, Rx provides Subscribe methods that take various combinations of OnNext, OnError and OnCompleted handlers in terms of delegates.

## Creating and subscribing to a simple sequence

The following sample uses the range operator of the Observable type to create a simple observable collection of numbers. The observer subscribes to this collection using the Subscribe method of the Observable class, and provides actions that are delegates which handle OnNext, OnCompleted and OnError.

The range operator has several overloads. In our example, it creates a sequence of integers that starts with x and produces y sequential numbers afterwards.

As soon as the subscription happens, the values are sent to the observer. The OnNext delegate then prints out the values.

      auto values1 = rxcpp::Range(1, 10);
      rxcpp::from(values1)
      .for_each(
      [](int p) {
      cout }); 

When an observer subscribes to an observable sequence, the thread calling the subscribe method can be different from the thread in which the sequence runs till completion. Therefore, the subscribe call is asynchronous in that the caller is not blocked until the observation of the sequence completes. This will be covered in more details in the Using Schedulers topic.

Notice that the subscribe method returns a Disposable, so that you can unsubscribe to a sequence and dispose of it easily. When you invoke the Dispose method on the observable sequence, the observer will stop listening to the observable for data. Normally, you do not need to explicitly call Dispose unless you need to unsubscribe early, or when the source observable sequence has a longer life span than the observer. Subscriptions in Rx are designed for fire-and-forget scenarios without the usage of a finalizer. When the Disposable instance is collected by the garbage collector, Rx does not automatically dispose of the subscription. However, note that the default behavior of the Observable operators is to dispose of the subscription as soon as possible (i.e, when an OnCompleted or OnError messages is published).

In addition to creating an observable sequence from scratch, you can convert existing enumerators, C++ events and asynchronous patterns into observable sequences. The other topics in this section will show you how to do this.

Notice that this topic only shows you a few operators that can create an observable sequence from scratch. To learn more about other LINQ operators, see Query Observable Collections using LINQ Operators.

## Converting an Enumerable Collection to an Observable Sequence

Using the Iterate operator, you can convert an array colection to an observable sequence and subscribe to it.

      std::array a={1, 2, 3};
      auto values1 = rxcpp::Iterate(a);

      rxcpp::from(values1)
      .for_each(
      [](int p) {
      cout });


### See Also

Query Observable Collections using LINQ Operators

We have converted existing C++ events into observable sequences to subscribe to them. In this topic, we will look at the first-class nature of observable sequences as Observable objects, in which generic LINQ operators are supplied by the Rx header-only library to manipulate these objects. Most operators take an observable sequence and perform some logic on it and output another observable sequence. In addition, as you can see from our code samples, you can even chain multiple operators on a source sequence to tweak the resulting sequence to your exact requirement.

## Using Different Operators

We have already used the Create and Generate operators in previous topics to create and return simple sequences. In this topic, we will use other LINQ operators of the Observable type so that you can filter, group and transform data. Such operators take observable sequence(s) as input, and produce observable sequence(s) as output.

## Combining different sequences

In this section, we will examine some of the operators that combine various observable sequences into a single observable sequence. Notice that data are not transformed when we combine sequences.

In the following sample, we use the concat operator to combine two sequences into a single sequence and subscribe to it.

      auto input1 = std::make_shared();
      auto input2 = std::make_shared();
      auto output = std::make_shared();

      auto values1 = rxcpp::Range(1); // infinite (until overflow) stream of integers
      auto s1 = rxcpp::from(values1)
      .subscribe_on(input1)
      .select([](int prime) ->; std::tuple { return std::make_tuple("1:", prime);})
      .take(3);

      auto values2 = rxcpp::Range(1); // infinite (until overflow) stream of integers
      auto s2 = rxcpp::from(values2)
      .subscribe_on(input2)
      .select([](int prime) ->; std::tuple { return std::make_tuple("2:", prime);})
      .take(3);

      rxcpp::from(s1)
      .concat(s2)
      .observe_on(output)
      .for_each(rxcpp::MakeTupleDispatch(
      [](const char* s, int p) {
      cout }));


Notice that the resultant sequence is 1,2,3,1,2,3. This is because when you use the concat operator, the 2nd sequence (source2) will not be active until after the 1st sequence (source1) has finished pushing all its values. It is only after source1 has completed, then source2 will start to push values to the resultant sequence. The subscriber will then get all the values from the resultant sequence.

Compare this with the merge operator. If you run the following sample code, you will get 1,1,2,2,3,3. This is because the two sequences are active at the same time and values are pushed out as they occur in the sources. The resultant sequence only completes when the last source sequence has finished pushing values.

Notice that for Merge to work, all the source observable sequences need to be of the same type of Observable. The resultant sequence will be of the type Observable. If source1 produces an OnError in the middle of the sequence, then the resultant sequence will complete immediately.

` auto input1 = std::make_shared();
auto input2 = std::make_shared();
auto output = std::make_shared();

auto values1 = rxcpp::Range(1); // infinite (until overflow) stream of integers
auto s1 = rxcpp::from(values1)
.subscribe_on(input1)
.select([](int data) -&gt; std::tuple { return std::make_tuple("1: ", data);});

auto values2 = rxcpp::Range(1); // infinite (until overflow) stream of integers
rxcpp::from(values2)
.subscribe_on(input1)
.select([](int data) -&gt; std::tuple { return std::make_tuple("2: ", data);})
.merge(s1)
.take(6)
.observe_on(output)
.for_each(rxcpp::MakeTupleDispatch(
[](const char* s, int p) {
cout }));

`

Notice that for these combination operators to work, all the observable sequences need to be of the same type.

This section describes the Subject type implemented by Reactive Extensions. It also describes various implementations of Subject which serves different purposes.

### In This Section

1. Using Subjects

The Subject type implements both Observable and Observer, in the sense that it is both an observer and an observable. You can use a subject to subscribe all the observers, and then subscribe the subject to a backend data source. In this way, the subject can act as a proxy for a group of subscribers and a source. You can use subjects to implement a custom observable with caching, buffering and time shifting. In addition, you can use subjects to broadcast data to multiple subscribers.

By default, subjects do not perform any synchronization across threads. They do not take a scheduler but rather assume that all serialization and grammatical correctness are handled by the caller of the subject. A subject simply broadcasts to all subscribed observers in the thread-safe list of subscribers. Doing so has the advantage of reducing overhead and improving performance. If, however, you want to synchronize outgoing calls to observers using a scheduler, you can use the Synchronize method to do so.

## Different types of Subjects

The Subject type in the Rx library is a basic implementation of the Subject interface (you can also implement the Subject interface to create your own subject types). There are other implementations of Subject that offer different functionalities. All of these types store some (or all of) values pushed to them via OnNext, and broadcast it back to its observers. This means that if you subscribe to any of these more than once (i.e. subscribe -&gt; unsubscribe -&gt; subscribe again), you will see at least one of the same value again.

This section describes how you can use a scheduler to control when to start a sequence or subscribe to an event.

The various Scheduler types provided by Rx are:

ImmediateScheduler: Default scheduler, pushes notifications as they are recieved.

EventLoopScheduler: Used when creating a separate thread for Rx sequences.

A scheduler controls when a subscription starts and when notifications are published. It consists of three components. It is first a data structure. When you schedule for tasks to be completed, they are put into the scheduler for queueing based on priority or other criteria. It also offers an execution context which denotes where the task is executed (e.g., in the thread pool, current thread, or in another app domain). Lastly, it has a clock which provides a notion of time for itself (by accessing the Now property of a scheduler). Tasks being scheduled on a particular scheduler will adhere to the time denoted by that clock only.

## Using Schedulers

You may have already used schedulers in your Rx code without explicitly stating the type of schedulers to be used. This is because all Observable operators that deal with concurrency have multiple overloads. If you do not use the overload which takes a scheduler as an argument, Rx will pick a default scheduler by using the principle of least concurrency. This means that the scheduler which introduces the least amount of concurrency that satisfies the needs of the operator is chosen. For example, for operators returning an observable with a finite and small number of messages, Rx calls ImmediateScheduler. For operators returning a potentially large or infinite number of messages, CurrentThread is called.

In the following example, the source observable sequences are each running in their own threads using EventLoopScheduler.

` auto input1 = std::make_shared();
auto input2 = std::make_shared();
auto output = std::make_shared();

auto values1 = rxcpp::Range(1); // infinite (until overflow) stream of integers
auto s1 = rxcpp::from(values1)
.subscribe_on(input1)
.select([](int data) -&gt; std::tuple { return std::make_tuple("1:", data);})
.take(3);

auto values2 = rxcpp::Range(1); // infinite (until overflow) stream of integers
auto s2 = rxcpp::from(values2)
.subscribe_on(input2)
.select([](int data) -&gt; std::tuple { return std::make_tuple("2:", data);})
.take(3);

rxcpp::from(s1)
.concat(s2)
.observe_on(output)
.for_each(rxcpp::MakeTupleDispatch(
[](const char* s, int p) {
cout }));

`

This will queue up on the observer quickly. We can improve this code by using the observe_on operator, which allows you to specify the context that you want to use to send pushed notifications (OnNext) to observers. By default, the observe_on operator ensures that OnNext will be called as many times as possible on the current thread. You can use its overloads and redirect the OnNext outputs to a different context. In addition, you can use the subscribe_on operator to return a proxy observable that delegates actions to a specific scheduler. For example, for a UI-intensive application, you can delegate all background operations to be performed on a scheduler running in the background by using subscribe_on and passing to it a Concurrency.EventLoopScheduler.

You should also note that by using the observe_on operator, an action is scheduled for each message that comes through the original observable sequence. This potentially changes timing information as well as puts additional stress on the system. If you have a query that composes various observable sequences running on many different execution contexts, and you are doing filtering in the query, it is best to place observe_on later in the query. This is because a query will potentially filter out a lot of messages, and placing the observe_on operator earlier in the query would do extra work on messages that would be filtered out anyway. Calling the observe_on operator at the end of the query will create the least performance impact.

You can extend Rx by adding new operators for operations that are not provided by the LINQ library, or by creating your own implementation of standard query operators to improve readability and performance. Writing a customized version of a standard LINQ operator is useful when you want to operate with in-memory objects and when the intended customization does not require a comprehensive view of the query.

## Creating New Operators

LINQ offers a full set of operators that cover most of the possible operations on a set of entities. However, you might need an operator to add a particular semantic meaning to your queryespecially if you can reuse that same operator several times in your code.

By reusing existing LINQ operators when you build a new one, you can take advantage of the existing performance or exception handling capabilities implemented in the Rx libraries.

When writing a custom operator, it is good practice not to leave any disposables unused; otherwise, you may find that resources could actually be leaked and cancellation may not work correctly.

## Customizing Existing Operators

Adding new operators to LINQ is a way to extend its capabilities. However, you can also improve code readability by wrapping existing operators into more specialized and meaningful ones.

   [1]: http://msdn.microsoft.com/en-us/data/gg577609
   [2]: http://msdn.microsoft.com/en-us/library/ff431792(VS.92).aspx
   [3]: http://msdn.microsoft.com/en-us/library/ff707857(v=VS.92).aspx
   [4]: http://blogs.msdn.com/b/rxteam/archive/2010/10/28/rx-for-windows-phone-7.aspx
  
  