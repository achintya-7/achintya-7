# Hello there, I'm Achintya <img src="https://raw.githubusercontent.com/aemmadi/aemmadi/master/wave.gif" width="30px">


I am Achintya, currently persuing B.Tech Computer Science. I am intrested in Machine Learning, App Development. I am a huge Open Source advocate and is always open to collaborate on new projetcs. Find out more about me & feel free to connect with me here:

[![Linkedin Badge](https://img.shields.io/badge/-Achintya-darkblue?style=flat-square&logo=Linkedin&logoColor=white&link=https://www.linkedin.com/in/achintya-singh-4b4563200/)](https://www.linkedin.com/in/achintya-singh-4b4563200/)
[![Twitter Badge](https://img.shields.io/badge/-Achintya-blue?style=flat-square&logo=twitter&logoColor=white&link=https://twitter.com/achintya2205)](https://twitter.com/achintya2205)
[![Gmail Badge](https://img.shields.io/badge/-achintya22052000@gmail.com-c14438?style=flat-square&logo=Gmail&logoColor=white&link=mailto:achintya22052000@gmail.com)](mailto:achintya22052000@gmail.com)
[![Website Badge](https://img.shields.io/badge/-Portfolio-grey?style=flat-square&logo=Github&logoColor=white&link=https://achintya-7.github.io/)](https://achintya-7.github.io/)

[![Achintya's github activity graph](https://activity-graph.herokuapp.com/graph?username=achintya-7&theme=xcode)](https://git.io/kaiwalyakoparkar)

# Blogs
<!-- BLOGPOSTS:START -->## 
 - 🌮 [Google Maps in your Flutter App](https://achintya-7.hashnode.dev/google-maps-in-your-flutter-app) - &lt;h1 id=&quot;heading-what-we-will-build&quot;&gt;What we will build&lt;/h1&gt;
&lt;p&gt;We are going to make a simple Maps App which will have 2 Form fields with autocomplete from where the user can add 2 locations. Then we will display a PolyLine/Route between those 2 places on the GoogleMap Widget.&lt;/p&gt;
&lt;h1 id=&quot;heading-requirements-and-pre-requisites&quot;&gt;Requirements and Pre-Requisites&lt;/h1&gt;
&lt;ul&gt;
&lt;li&gt;A machine with Flutter installed&lt;/li&gt;
&lt;li&gt;Google account for Google Cloud Console&lt;/li&gt;
&lt;li&gt;Google Maps SDK&lt;/li&gt;
&lt;li&gt;Places API&lt;/li&gt;
&lt;li&gt;Directions API&lt;/li&gt;
&lt;/ul&gt;
&lt;h1 id=&quot;heading-getting-google-maps-and-places-api&quot;&gt;Getting Google Maps and Places API&lt;/h1&gt;
&lt;p&gt;We can get the &lt;strong&gt;&quot;Google Maps API&quot;&lt;/strong&gt;  from Google Cloud Console under the &lt;strong&gt;&quot;APIs and Services&quot;&lt;/strong&gt; section. You will need to make a project once to use the Maps SDK.&lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1654099586999/GptfCtUu5.png&quot; alt=&quot;image.png&quot; /&gt;&lt;/p&gt;
&lt;p&gt;Click on Library and search for &lt;strong&gt;&quot;Maps SDK for Android&quot;&lt;/strong&gt; and enable it. This will enable the API for our selected Project but we still haven&#39;t got the key to use this API. We also need to add the &lt;strong&gt;&quot;Places API&quot;&lt;/strong&gt; similarly to get the predictions of locations. &lt;/p&gt;
&lt;blockquote&gt;
&lt;p&gt;Note: To use it on iOS, you also have to enable  &lt;strong&gt;&quot;Maps SDK for iOS&quot;&lt;/strong&gt; separately.&lt;/p&gt;
&lt;/blockquote&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1654100076219/OSn4BGB2T.png&quot; alt=&quot;image.png&quot; /&gt;&lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1654164774668/TPu58Kw5r.png&quot; alt=&quot;image.png&quot; /&gt;&lt;/p&gt;
&lt;p&gt;We can make our new key by going into Credentials and clicking &lt;strong&gt;&quot;CREATE CREDENTIALS&quot;&lt;/strong&gt; and selecting &lt;strong&gt;&quot;API key&quot;&lt;/strong&gt;. A popup box will open with your required key. &lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1654100620049/3RQXTz8Fo.png&quot; alt=&quot;image.png&quot; /&gt;&lt;/p&gt;
&lt;p&gt;Voila! We got the API key and now let&#39;s move forward to implement it in our Flutter app. &lt;/p&gt;
&lt;h1 id=&quot;heading-displaying-a-map-in-our-app&quot;&gt;Displaying a Map in our App&lt;/h1&gt;
&lt;p&gt;Let&#39;s build a flutter project and open it in an IDE. I&#39;ll be using VSCode for this blog. If you are also using VSCode, you can copy the commands below and paste them into your terminal.&lt;/p&gt;
&lt;pre&gt;&lt;code&gt;flutter &lt;span class=&quot;hljs-keyword&quot;&gt;create&lt;/span&gt; maps_demo
cd maps_demo
code .
&lt;/code&gt;&lt;/pre&gt;&lt;p&gt;Let&#39;s open our project and save the API key into a &lt;strong&gt;&quot;.env&quot;&lt;/strong&gt; file. You can create the &lt;strong&gt;&quot;.env&quot;&lt;/strong&gt; file in your root directory of the project. Transform the main function into this to load the data from the &lt;strong&gt;&quot;.env&quot;&lt;/strong&gt; file. &lt;/p&gt;
&lt;pre&gt;&lt;code&gt;&lt;span class=&quot;hljs-function&quot;&gt;Future &lt;span class=&quot;hljs-title&quot;&gt;main&lt;/span&gt;&lpar;&lt;span class=&quot;hljs-params&quot;&gt;&lt;/span&gt;&rpar; &lt;span class=&quot;hljs-keyword&quot;&gt;async&lt;/span&gt;&lt;/span&gt; {
  &lt;span class=&quot;hljs-keyword&quot;&gt;await&lt;/span&gt; dotenv.load&lpar;fileName: &lt;span class=&quot;hljs-string&quot;&gt;&quot;.env&quot;&lt;/span&gt;&rpar;;
  runApp&lpar;&lt;span class=&quot;hljs-function&quot;&gt;&lt;span class=&quot;hljs-keyword&quot;&gt;const&lt;/span&gt; &lt;span class=&quot;hljs-title&quot;&gt;MyApp&lt;/span&gt;&lpar;&lt;span class=&quot;hljs-params&quot;&gt;&lt;/span&gt;&rpar;&rpar;&lt;/span&gt;;
}
&lt;/code&gt;&lt;/pre&gt;&lt;p&gt;We also have to add the API key to our AndroidManifest.xml file. Add this snipped into the manifest file and also your API key in the required field i.e. &lt;strong&gt;android:value&lt;/strong&gt;.&lt;/p&gt;
&lt;pre&gt;&lt;code&gt;&lt;span class=&quot;hljs-operator&quot;&gt;&amp;lt;&lt;/span&gt;manifest ...
  &lt;span class=&quot;hljs-operator&quot;&gt;&amp;lt;&lt;/span&gt;application ...
    &lt;span class=&quot;hljs-operator&quot;&gt;&amp;lt;&lt;/span&gt;meta&lt;span class=&quot;hljs-operator&quot;&gt;-&lt;/span&gt;data android:name&lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt;&lt;span class=&quot;hljs-string&quot;&gt;&quot;com.google.android.geo.API_KEY&quot;&lt;/span&gt;
               android:value&lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt;&lt;span class=&quot;hljs-string&quot;&gt;&quot;YOUR ANDROID API KEY HERE&quot;&lt;/span&gt;&lt;span class=&quot;hljs-operator&quot;&gt;/&lt;/span&gt;&lt;span class=&quot;hljs-operator&quot;&gt;&amp;gt;&lt;/span&gt;
&lt;/code&gt;&lt;/pre&gt;&lt;blockquote&gt;
&lt;p&gt;You might also need to set the minSdkVersion to 21 in the app-level build.gradle file&lt;/p&gt;
&lt;/blockquote&gt;
&lt;p&gt;Create a new page with &lt;strong&gt;Statefulwidget&lt;/strong&gt; and define the following variables. We have taken New Delhi as the default location which will be displayed when the &lt;strong&gt;GoogleMap&lt;/strong&gt; widget is rendered. &lt;/p&gt;
&lt;pre&gt;&lt;code&gt;&lt;span class=&quot;hljs-attribute&quot;&gt;final&lt;/span&gt; Completer&amp;lt;GoogleMapController&amp;gt; _controllerGoogleMap = Completer&lpar;&rpar;;
&lt;span class=&quot;hljs-attribute&quot;&gt;GoogleMapController&lt;/span&gt;? _googleMapController;
&lt;span class=&quot;hljs-attribute&quot;&gt;static&lt;/span&gt; const LatLng _center = LatLng&lpar;&lt;span class=&quot;hljs-number&quot;&gt;28&lt;/span&gt;.&lt;span class=&quot;hljs-number&quot;&gt;61992743538245&lt;/span&gt;, &lt;span class=&quot;hljs-number&quot;&gt;77&lt;/span&gt;.&lt;span class=&quot;hljs-number&quot;&gt;20905101733563&lt;/span&gt;&rpar;;
&lt;/code&gt;&lt;/pre&gt;&lt;p&gt;Now we can add the GoogleMap widget to our body. The best way to implement the &lt;strong&gt;&lt;code&gt;GoogleMap&lt;/code&gt;&lt;/strong&gt; widget is to use it in a &lt;strong&gt;&lt;code&gt;Stack&lt;/code&gt;&lt;/strong&gt; widget.&lt;/p&gt;
&lt;pre&gt;&lt;code&gt;&lt;span class=&quot;hljs-string&quot;&gt;GoogleMap&lpar;&lt;/span&gt;
  &lt;span class=&quot;hljs-attr&quot;&gt;onMapCreated:&lt;/span&gt; &lt;span class=&quot;hljs-string&quot;&gt;&lpar;GoogleMapController&lt;/span&gt; &lt;span class=&quot;hljs-string&quot;&gt;controller&rpar;&lt;/span&gt; {
    &lt;span class=&quot;hljs-string&quot;&gt;_controllerGoogleMap.complete&lpar;controller&rpar;;&lt;/span&gt;
    &lt;span class=&quot;hljs-string&quot;&gt;_googleMapController&lt;/span&gt; &lt;span class=&quot;hljs-string&quot;&gt;=&lt;/span&gt; &lt;span class=&quot;hljs-string&quot;&gt;controller;&lt;/span&gt;
  }&lt;span class=&quot;hljs-string&quot;&gt;,&lt;/span&gt;
  &lt;span class=&quot;hljs-attr&quot;&gt;initialCameraPosition:&lt;/span&gt; &lt;span class=&quot;hljs-string&quot;&gt;const&lt;/span&gt; &lt;span class=&quot;hljs-string&quot;&gt;CameraPosition&lpar;&lt;/span&gt;
    &lt;span class=&quot;hljs-attr&quot;&gt;target:&lt;/span&gt; &lt;span class=&quot;hljs-string&quot;&gt;_center,&lt;/span&gt;
    &lt;span class=&quot;hljs-attr&quot;&gt;zoom:&lt;/span&gt; &lt;span class=&quot;hljs-number&quot;&gt;11.0&lt;/span&gt;&lt;span class=&quot;hljs-string&quot;&gt;,&lt;/span&gt;
  &lt;span class=&quot;hljs-string&quot;&gt;&rpar;,&lt;/span&gt;
&lt;span class=&quot;hljs-string&quot;&gt;&rpar;&lt;/span&gt;
&lt;/code&gt;&lt;/pre&gt;&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1654104855004/gdNG0EQaf.png&quot; alt=&quot;image.png&quot; /&gt;&lt;/p&gt;
&lt;p&gt;We have successfully added the map to our app. Let&#39;s work on adding some features to it.&lt;/p&gt;
&lt;h1 id=&quot;heading-implementing-location-autocomplete&quot;&gt;Implementing Location Autocomplete&lt;/h1&gt;
&lt;p&gt;We will use the Places API to get predictions of the locations. We will use a TextForm widget to get the location queries from the user and a ListView widget to display the recommended places. &lt;/p&gt;
&lt;p&gt;We will now need to add new variables for this, basically an empty list and GooglePlace object. Also, form an initstate to initialize the GooglePlace and all the late Objects.&lt;/p&gt;
&lt;pre&gt;&lt;code&gt;List&lt;span class=&quot;hljs-operator&quot;&gt;&amp;lt;&lt;/span&gt;AutocompletePrediction&lt;span class=&quot;hljs-operator&quot;&gt;&amp;gt;&lt;/span&gt; predictions &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; [];
final _startingLocationController &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; TextEditingController&lpar;&rpar;;
final _endingLocationController &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; TextEditingController&lpar;&rpar;;
DetailsResult? startPosition;
DetailsResult? endPosition;
late GooglePlace googlePlace;
Timer? debounce;
late FocusNode startFocusNode;
late FocusNode endFocusNode;

@&lt;span class=&quot;hljs-keyword&quot;&gt;override&lt;/span&gt;
void initState&lpar;&rpar; {
  &lt;span class=&quot;hljs-built_in&quot;&gt;super&lt;/span&gt;.initState&lpar;&rpar;;
  googlePlace &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; GooglePlace&lpar;dotenv.env[&lt;span class=&quot;hljs-string&quot;&gt;&#39;API_key&#39;&lt;/span&gt;]&lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt;&rpar;;
  startFocusNode &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; FocusNode&lpar;&rpar;;
  endFocusNode &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; FocusNode&lpar;&rpar;;
}

@&lt;span class=&quot;hljs-keyword&quot;&gt;override&lt;/span&gt;
void dispose&lpar;&rpar; {
  &lt;span class=&quot;hljs-built_in&quot;&gt;super&lt;/span&gt;.dispose&lpar;&rpar;;
  startFocusNode.dispose&lpar;&rpar;;
  endFocusNode.dispose&lpar;&rpar;;
  _googleMapController&lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt;.dispose&lpar;&rpar;;
}
&lt;/code&gt;&lt;/pre&gt;&lt;p&gt;Let&#39;s create a function to get predictions from a given value. The value will be taken from the TextEditingController and the predictions will maid according to it.&lt;/p&gt;
&lt;pre&gt;&lt;code&gt;autoComplete&lpar;String value&rpar; async {
  &lt;span class=&quot;hljs-keyword&quot;&gt;var&lt;/span&gt; result &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; await googlePlace.autocomplete.get&lpar;value&rpar;;
  &lt;span class=&quot;hljs-keyword&quot;&gt;if&lt;/span&gt; &lpar;result &lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt;&lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; null &lt;span class=&quot;hljs-operator&quot;&gt;&amp;amp;&lt;/span&gt;&lt;span class=&quot;hljs-operator&quot;&gt;&amp;amp;&lt;/span&gt; result.predictions &lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt;&lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; null&rpar; {
    setState&lpar;&lpar;&rpar; {
      predictions &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; result.predictions!;
    }&rpar;;
  }
}
&lt;/code&gt;&lt;/pre&gt;&lt;p&gt;Let&#39;s add a TextForm to get these values and call the function every time the value in it is changed. We will also make a similar form for taking the destination as well.&lt;/p&gt;
&lt;pre&gt;&lt;code&gt;&lt;span class=&quot;hljs-comment&quot;&gt;// TextForm for getting start location&lt;/span&gt;
TextField&lpar;
  focusNode: startFocusNode,
  controller: _startingLocationController,
  decoration: InputDecoration&lpar;
    suffixIcon: _startingLocationController.text.isNotEmpty
          ? IconButton&lpar;
              onPressed: &lpar;&rpar; {
                setState&lpar;&lpar;&rpar; {
                  predictions &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; [];
                  _startingLocationController.clear&lpar;&rpar;;
                }&rpar;;
              },
              icon: const Icon&lpar;Icons.clear_outlined&rpar;&rpar;
          : null,
      fillColor: Colors.white,
      filled: &lt;span class=&quot;hljs-literal&quot;&gt;true&lt;/span&gt;,
      prefixIcon: const Icon&lpar;CupertinoIcons.location_solid&rpar;,
      hintText: &lt;span class=&quot;hljs-string&quot;&gt;&#39;Starting Location&#39;&lt;/span&gt;&rpar;,
  onChanged: &lpar;value&rpar; {
    &lt;span class=&quot;hljs-keyword&quot;&gt;if&lt;/span&gt; &lpar;value.isNotEmpty&rpar; {
      autoComplete&lpar;value&rpar;;
    } &lt;span class=&quot;hljs-keyword&quot;&gt;else&lt;/span&gt; {
      setState&lpar;&lpar;&rpar; {
        predictions &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; [];
        startPosition &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; null;
      }&rpar;;         
    }
  },
&rpar;,

&lt;span class=&quot;hljs-comment&quot;&gt;// TextForm for getting end location&lt;/span&gt;
TextField&lpar;
  focusNode: endFocusNode,
  controller: _endingLocationController,
  decoration: InputDecoration&lpar;
    suffixIcon: _endingLocationController.text.isNotEmpty
        ? IconButton&lpar;
            onPressed: &lpar;&rpar; {
              setState&lpar;&lpar;&rpar; {
                predictions &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; [];
                _startingLocationController.clear&lpar;&rpar;;
              }&rpar;;
            },
            icon: const Icon&lpar;Icons.clear_outlined&rpar;&rpar;
        : null,
    fillColor: Colors.white,
    filled: &lt;span class=&quot;hljs-literal&quot;&gt;true&lt;/span&gt;,
    prefixIcon: const Icon&lpar;CupertinoIcons.location_solid&rpar;,
    hintText: &lt;span class=&quot;hljs-string&quot;&gt;&#39;Ending Location&#39;&lt;/span&gt;&rpar;,
  onChanged: &lpar;value&rpar; {
    &lt;span class=&quot;hljs-keyword&quot;&gt;if&lt;/span&gt; &lpar;value.isNotEmpty&rpar; {
      autoComplete&lpar;value&rpar;;
    } &lt;span class=&quot;hljs-keyword&quot;&gt;else&lt;/span&gt; {
      setState&lpar;&lpar;&rpar; {
        predictions &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; [];
        startPosition &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; null;
      }&rpar;;
    }
  },
&rpar;,
&lt;/code&gt;&lt;/pre&gt;&lt;p&gt;Now, we will make a &lt;strong&gt;ListView&lt;/strong&gt; to show all the predictions. The user can then click on a list tile and the name of the place will be selected. The value of start and end will be selected based on &lt;strong&gt;FocusNode&lt;/strong&gt; selected.  &lt;/p&gt;
&lt;pre&gt;&lt;code&gt;ListView.builder&lpar;
  shrinkWrap: &lt;span class=&quot;hljs-literal&quot;&gt;true&lt;/span&gt;,
  itemCount: predictions.&lt;span class=&quot;hljs-built_in&quot;&gt;length&lt;/span&gt;,
  itemBuilder: &lpar;BuildContext context, &lt;span class=&quot;hljs-keyword&quot;&gt;int&lt;/span&gt; index&rpar; {
    &lt;span class=&quot;hljs-keyword&quot;&gt;return&lt;/span&gt; Padding&lpar;
      padding: const EdgeInsets.only&lpar;top: &lt;span class=&quot;hljs-number&quot;&gt;4&lt;/span&gt;&rpar;,
      child: ElevatedButton&lpar;
        onPressed: &lpar;&rpar; async {
          final placeId &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; predictions[index].placeId!;
          final details &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; await googlePlace.details.get&lpar;placeId&rpar;;
          &lt;span class=&quot;hljs-keyword&quot;&gt;if&lt;/span&gt; &lpar;details &lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt;&lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; null &lt;span class=&quot;hljs-operator&quot;&gt;&amp;amp;&lt;/span&gt;&lt;span class=&quot;hljs-operator&quot;&gt;&amp;amp;&lt;/span&gt;
              details.result &lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt;&lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; null &lt;span class=&quot;hljs-operator&quot;&gt;&amp;amp;&lt;/span&gt;&lt;span class=&quot;hljs-operator&quot;&gt;&amp;amp;&lt;/span&gt;
              mounted&rpar; {
            &lt;span class=&quot;hljs-keyword&quot;&gt;if&lt;/span&gt; &lpar;startFocusNode.hasFocus&rpar; {
              setState&lpar;&lpar;&rpar; {
                startPosition &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; details.result;
                _startingLocationController.text &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt;
                    details.result!.&lt;span class=&quot;hljs-built_in&quot;&gt;name&lt;/span&gt;!.toString&lpar;&rpar;;
                predictions &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; [];
                debugPrint&lpar;&lt;span class=&quot;hljs-string&quot;&gt;&#39;Name of Location is : ${_startingLocationController.text}&#39;&lt;/span&gt;&rpar;;
                debugPrint&lpar;&lt;span class=&quot;hljs-string&quot;&gt;&#39;location is : $startPosition&#39;&lt;/span&gt;&rpar;;
              }&rpar;;
            } &lt;span class=&quot;hljs-keyword&quot;&gt;else&lt;/span&gt; {
              setState&lpar;&lpar;&rpar; {
                endPosition &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; details.result;
                _endingLocationController.text &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; details.result!.&lt;span class=&quot;hljs-built_in&quot;&gt;name&lt;/span&gt;!.toString&lpar;&rpar;;
                predictions &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; [];
              }&rpar;;
            }
            FocusManager.instance.primaryFocus?.unfocus&lpar;&rpar;;
          }
        },
        child: ListTile&lpar;
          leading: const CircleAvatar&lpar;
            child: Icon&lpar;Icons.pin_drop&rpar;,
          &rpar;,
          isThreeLine: &lt;span class=&quot;hljs-literal&quot;&gt;false&lt;/span&gt;,
          title: Text&lpar;
            predictions[index].description.toString&lpar;&rpar;,
            maxLines: &lt;span class=&quot;hljs-number&quot;&gt;2&lt;/span&gt;,
            overflow: TextOverflow.ellipsis,
          &rpar;,
        &rpar;,
      &rpar;,
    &rpar;;
  },
&rpar;,
&lt;/code&gt;&lt;/pre&gt;&lt;p&gt;Now, to prevent the recurring use of API all the time, we will use a &lt;strong&gt;debounce&lt;/strong&gt;. Debounce is a timer which will wait for some time before sending a new request to the API. This helps reduce the cost of API usage. We will implement it in the &lt;strong&gt;onChanged &lt;/strong&gt;state of both the &lt;strong&gt;TextForms&lt;/strong&gt;.&lt;/p&gt;
&lt;pre&gt;&lt;code&gt;onChanged: &lpar;value&rpar; {
  &lt;span class=&quot;hljs-keyword&quot;&gt;if&lt;/span&gt; &lpar;debounce?.isActive ?? &lt;span class=&quot;hljs-literal&quot;&gt;false&lt;/span&gt;&rpar; debounce&lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt;.cancel&lpar;&rpar;;
  debounce &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; Timer&lpar;const Duration&lpar;microseconds: &lt;span class=&quot;hljs-number&quot;&gt;1000&lt;/span&gt;&rpar;, &lpar;&rpar; {
    &lt;span class=&quot;hljs-keyword&quot;&gt;if&lt;/span&gt; &lpar;value.isNotEmpty&rpar; {
      autoComplete&lpar;value&rpar;;
    } &lt;span class=&quot;hljs-keyword&quot;&gt;else&lt;/span&gt; {
      &lt;span class=&quot;hljs-comment&quot;&gt;//clear the search&lt;/span&gt;
      setState&lpar;&lpar;&rpar; {
        predictions &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; [];
        endPosition &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; null;
      }&rpar;;
    }
  }&rpar;;
}
&lt;/code&gt;&lt;/pre&gt;&lt;p&gt;Let&#39;s see how the app is working as of now.&lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1654169161211/DWdIAOgqX.gif&quot; alt=&quot;Blog1.gif&quot; /&gt;&lt;/p&gt;
&lt;h1 id=&quot;heading-drawing-a-route-between-2-locations&quot;&gt;Drawing a Route between 2 locations&lt;/h1&gt;
&lt;p&gt;To display a route between 2 locations, we use a PolyLine or a set of PolyLines and pass it to the &lt;strong&gt;GoogleMap&lt;/strong&gt; widget. A PolyLine is a list of all the points between two points. We will need another API for it called &lt;strong&gt;&quot;Directions API&quot;&lt;/strong&gt;. Just activate it on your Google Cloud Console and you are good to go.&lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1654237474104/4kgnysj2Q.png&quot; alt=&quot;image.png&quot; /&gt;&lt;/p&gt;
&lt;p&gt;Now let&#39;s define some new variables to start implementing this feature.&lt;/p&gt;
&lt;pre&gt;&lt;code&gt;Marker? _origin;
Marker? _destination;
List&lt;span class=&quot;hljs-operator&quot;&gt;&amp;lt;&lt;/span&gt;Marker&lt;span class=&quot;hljs-operator&quot;&gt;&amp;gt;&lt;/span&gt; markers &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; [];
Map&lt;span class=&quot;hljs-operator&quot;&gt;&amp;lt;&lt;/span&gt;PolylineId, Polyline&lt;span class=&quot;hljs-operator&quot;&gt;&amp;gt;&lt;/span&gt; polylines &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; {};
List&lt;span class=&quot;hljs-operator&quot;&gt;&amp;lt;&lt;/span&gt;LatLng&lt;span class=&quot;hljs-operator&quot;&gt;&amp;gt;&lt;/span&gt; polylineCoordinates &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; [];
PolylinePoints polylinePoints &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; PolylinePoints&lpar;&rpar;;
Polyline? polyline;
List&lt;span class=&quot;hljs-operator&quot;&gt;&amp;lt;&lt;/span&gt;Polyline&lt;span class=&quot;hljs-operator&quot;&gt;&amp;gt;&lt;/span&gt; polylineValues &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; [];
&lt;/code&gt;&lt;/pre&gt;&lt;p&gt;Now let&#39;s write a function to draw &lt;strong&gt;PolyLine&lt;/strong&gt; on our map. We will pass two &lt;strong&gt;DetailResult&lt;/strong&gt; objects to it which we got from both the &lt;strong&gt;TextForm&lt;/strong&gt;.&lt;/p&gt;
&lt;pre&gt;&lt;code&gt;drawPolyLine&lpar;DetailsResult start, DetailsResult end&rpar; async {
  polylines.clear&lpar;&rpar;;
  markers.clear&lpar;&rpar;;
  polylineCoordinates.clear&lpar;&rpar;;
  polylineValues.clear&lpar;&rpar;;

  _origin &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; Marker&lpar;
      markerId: const MarkerId&lpar;&lt;span class=&quot;hljs-string&quot;&gt;&#39;Origin&#39;&lt;/span&gt;&rpar;,
      infoWindow: const InfoWindow&lpar;title: &lt;span class=&quot;hljs-string&quot;&gt;&#39;Origin&#39;&lt;/span&gt;&rpar;,
      icon: BitmapDescriptor.defaultMarkerWithHue&lpar;BitmapDescriptor.hueGreen&rpar;,
      position: LatLng&lpar;start.geometry!.location!.lat!, start.geometry!.location!.lng!&rpar;&rpar;;
  markers.add&lpar;_origin&lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt;&rpar;;

  _destination &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; Marker&lpar;
      markerId: const MarkerId&lpar;&lt;span class=&quot;hljs-string&quot;&gt;&#39;Destination&#39;&lt;/span&gt;&rpar;,
      infoWindow: const InfoWindow&lpar;title: &lt;span class=&quot;hljs-string&quot;&gt;&#39;Destination&#39;&lt;/span&gt;&rpar;,
      icon: BitmapDescriptor.defaultMarkerWithHue&lpar;BitmapDescriptor.hueRed&rpar;,
      position:  LatLng&lpar;end.geometry!.location!.lat!, end.geometry!.location!.lng!&rpar;&rpar;;
  markers.add&lpar;_destination&lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt;&rpar;;

  await getPolyLine&lpar;&rpar;;

  _googleMapController&lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt;.moveCamera&lpar;CameraUpdate.newLatLngBounds&lpar;
      MapUtils.boundsFromLatLngList&lpar;
          markers.map&lpar;&lpar;loc&rpar; &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt;&lt;span class=&quot;hljs-operator&quot;&gt;&amp;gt;&lt;/span&gt; loc.position&rpar;.toList&lpar;&rpar;&rpar;,
      &lt;span class=&quot;hljs-number&quot;&gt;1&lt;/span&gt;&rpar;&rpar;;

  polylineValues &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; List&lt;span class=&quot;hljs-operator&quot;&gt;&amp;lt;&lt;/span&gt;Polyline&lt;span class=&quot;hljs-operator&quot;&gt;&amp;gt;&lt;/span&gt;.of&lpar;polylines.values&rpar;;

  setState&lpar;&lpar;&rpar; {
    print&lpar;&lt;span class=&quot;hljs-string&quot;&gt;&#39;Length : &#39;&lt;/span&gt; &lt;span class=&quot;hljs-operator&quot;&gt;+&lt;/span&gt; polylineValues[&lt;span class=&quot;hljs-number&quot;&gt;0&lt;/span&gt;].toString&lpar;&rpar;&rpar;;
  }&rpar;;
}
&lt;/code&gt;&lt;/pre&gt;&lt;p&gt;This function will first assign two markers as &lt;strong&gt;Origin&lt;/strong&gt; and &lt;strong&gt;Destination&lt;/strong&gt; and add them to our &lt;strong&gt;markers&lt;/strong&gt; list. We will assign the required position from the &lt;strong&gt;startPosition&lt;/strong&gt; and &lt;strong&gt;endPosition&lt;/strong&gt;. It will also clear all the previous lists so as to prevent multiple previously drawn lines from rendering again after the state change when the function is called again.
Let&#39;s write the &lt;strong&gt;&lt;code&gt;getPolyLine&lpar;&rpar;&lt;/code&gt;&lt;/strong&gt; function which will draw the polyline from the given markers.&lt;/p&gt;
&lt;pre&gt;&lt;code&gt;getPolyLine&lpar;&rpar; async {
    PolylineResult result &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; await polylinePoints.getRouteBetweenCoordinates&lpar;
      dotenv.env[&lt;span class=&quot;hljs-string&quot;&gt;&#39;API_key&#39;&lt;/span&gt;]&lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt;,
      PointLatLng&lpar;startPosition&lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt;.geometry!.location!.lat!,
          startPosition&lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt;.geometry!.location!.lng!&rpar;,
      PointLatLng&lpar;endPosition&lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt;.geometry!.location!.lat!,
          endPosition&lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt;.geometry!.location!.lng!&rpar;,
    &rpar;;
    &lt;span class=&quot;hljs-keyword&quot;&gt;if&lt;/span&gt; &lpar;result.points.isNotEmpty&rpar; {
      &lt;span class=&quot;hljs-keyword&quot;&gt;for&lt;/span&gt; &lpar;&lt;span class=&quot;hljs-keyword&quot;&gt;var&lt;/span&gt; points in result.points&rpar; {
        polylineCoordinates.add&lpar;LatLng&lpar;points.latitude, points.longitude&rpar;&rpar;;
      }
      _addPolyLine&lpar;&rpar;;
    }
  }
&lt;/code&gt;&lt;/pre&gt;&lt;p&gt;Here we will use the start and end point Latitude and Longitude to get the result from the &lt;strong&gt;&quot;Directions API&quot;&lt;/strong&gt;. If there is a result provided by the API, we will call the &lt;strong&gt;&lt;code&gt;_addPolyLine&lpar;&rpar;&lt;/code&gt;&lt;/strong&gt; function to add the &lt;strong&gt;PolyLines&lt;/strong&gt; to a list so that the &lt;strong&gt;GoogleMap&lt;/strong&gt; widget can render it.&lt;/p&gt;
&lt;pre&gt;&lt;code&gt;_addPolyLine&lpar;&rpar; {
  PolylineId id &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; const PolylineId&lpar;&lt;span class=&quot;hljs-string&quot;&gt;&#39;poly&#39;&lt;/span&gt;&rpar;;
  polyline &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; Polyline&lpar;
      polylineId: id,
      color: Colors.purple,
      points: polylineCoordinates,
      width: &lt;span class=&quot;hljs-number&quot;&gt;3&lt;/span&gt;&rpar;;
  polylines[id] &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; polyline&lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt;;
  setState&lpar;&lpar;&rpar; {}&rpar;;
}
&lt;/code&gt;&lt;/pre&gt;&lt;p&gt;Now that we have the &lt;strong&gt;PolyLines&lt;/strong&gt; between 2 locations. We can render the line in our &lt;strong&gt;GoogleMap&lt;/strong&gt;. Now, let&#39;s form a button which will call the function &lt;strong&gt;&lt;code&gt;drawPolyLine&lpar;&rpar;&lt;/code&gt;&lt;/strong&gt;.&lt;/p&gt;
&lt;pre&gt;&lt;code&gt;Align&lpar;
  alignment: Alignment.bottomCenter,
  child: Padding&lpar;
    padding: const EdgeInsets.all&lpar;&lt;span class=&quot;hljs-number&quot;&gt;8.0&lt;/span&gt;&rpar;,
    child: ElevatedButton&lpar;
        onPressed: &lpar;&rpar; {
          &lt;span class=&quot;hljs-keyword&quot;&gt;if&lt;/span&gt; &lpar;startPosition &lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt;&lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; null &lt;span class=&quot;hljs-operator&quot;&gt;&amp;amp;&lt;/span&gt;&lt;span class=&quot;hljs-operator&quot;&gt;&amp;amp;&lt;/span&gt; endPosition &lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt;&lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; null&rpar; {
            drawPolyLine&lpar;startPosition&lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt;, endPosition&lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt;&rpar;;
          }
        },
        child: const Text&lpar;&lt;span class=&quot;hljs-string&quot;&gt;&quot;Search&quot;&lt;/span&gt;&rpar;&rpar;,
  &rpar;,
&rpar;
&lt;/code&gt;&lt;/pre&gt;&lt;p&gt;The function will only be called if both the &lt;strong&gt;startPosition&lt;/strong&gt; and &lt;strong&gt;endPosition&lt;/strong&gt; are not null. You can also add a Toast message to tell the user to add both locations.
In the function &lt;strong&gt;&lt;code&gt;drawPolyLine&lpar;&rpar;&lt;/code&gt;&lt;/strong&gt;, there is a code snippet which will move the camera of &lt;strong&gt;GoogleMap&lt;/strong&gt; to show both the markers.&lt;/p&gt;
&lt;pre&gt;&lt;code&gt;_googleMapController&lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt;.moveCamera&lpar;CameraUpdate.newLatLngBounds&lpar;
        MapUtils.boundsFromLatLngList&lpar;
            markers.map&lpar;&lpar;loc&rpar; &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt;&lt;span class=&quot;hljs-operator&quot;&gt;&amp;gt;&lt;/span&gt; loc.position&rpar;.toList&lpar;&rpar;&rpar;,
        &lt;span class=&quot;hljs-number&quot;&gt;1&lt;/span&gt;&rpar;&rpar;;
&lt;/code&gt;&lt;/pre&gt;&lt;p&gt;Here &lt;strong&gt;&lt;code&gt;MapUtils&lt;/code&gt;&lt;/strong&gt; is a class which will provide the &lt;strong&gt;LatLngBounds&lt;/strong&gt; to move the camera to a proper camera location. We will make a new dart file named &lt;strong&gt;&lt;code&gt;map_utils.dart&lt;/code&gt;&lt;/strong&gt; and add this class to it.&lt;/p&gt;
&lt;pre&gt;&lt;code&gt;&lt;span class=&quot;hljs-keyword&quot;&gt;import&lt;/span&gt; &lt;span class=&quot;hljs-string&quot;&gt;&#39;package:google_maps_flutter/google_maps_flutter.dart&#39;&lt;/span&gt;;

class MapUtils {
  static LatLngBounds boundsFromLatLngList&lpar;List&lt;span class=&quot;hljs-operator&quot;&gt;&amp;lt;&lt;/span&gt;LatLng&lt;span class=&quot;hljs-operator&quot;&gt;&amp;gt;&lt;/span&gt; list&rpar; {
    double? x0, x1, y0, y1;
    &lt;span class=&quot;hljs-keyword&quot;&gt;for&lt;/span&gt; &lpar;LatLng latLng in list&rpar; {
      &lt;span class=&quot;hljs-keyword&quot;&gt;if&lt;/span&gt; &lpar;x0 &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt;&lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; null&rpar; {
        x0 &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; x1 &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; latLng.latitude;
        y0 &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; y1 &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; latLng.longitude;
      } &lt;span class=&quot;hljs-keyword&quot;&gt;else&lt;/span&gt; {
        &lt;span class=&quot;hljs-keyword&quot;&gt;if&lt;/span&gt; &lpar;latLng.latitude &lt;span class=&quot;hljs-operator&quot;&gt;&amp;gt;&lt;/span&gt; x1&lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt;&rpar; x1 &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; latLng.latitude;
        &lt;span class=&quot;hljs-keyword&quot;&gt;if&lt;/span&gt; &lpar;latLng.latitude &lt;span class=&quot;hljs-operator&quot;&gt;&amp;lt;&lt;/span&gt; x0&rpar; x0 &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; latLng.latitude;
        &lt;span class=&quot;hljs-keyword&quot;&gt;if&lt;/span&gt; &lpar;latLng.longitude &lt;span class=&quot;hljs-operator&quot;&gt;&amp;gt;&lt;/span&gt; y1&lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt;&rpar; y1 &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; latLng.longitude;
        &lt;span class=&quot;hljs-keyword&quot;&gt;if&lt;/span&gt; &lpar;latLng.longitude &lt;span class=&quot;hljs-operator&quot;&gt;&amp;lt;&lt;/span&gt; y0&lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt;&rpar; y0 &lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt; latLng.longitude;
      }
    }
    &lt;span class=&quot;hljs-keyword&quot;&gt;return&lt;/span&gt; LatLngBounds&lpar;
        northeast: LatLng&lpar;x1&lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt; &lt;span class=&quot;hljs-operator&quot;&gt;+&lt;/span&gt; &lt;span class=&quot;hljs-number&quot;&gt;0&lt;/span&gt;&lt;span class=&quot;hljs-number&quot;&gt;.5&lt;/span&gt;, y1&lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt; &lt;span class=&quot;hljs-operator&quot;&gt;+&lt;/span&gt; &lt;span class=&quot;hljs-number&quot;&gt;0&lt;/span&gt;&lt;span class=&quot;hljs-number&quot;&gt;.5&lt;/span&gt;&rpar;, southwest: LatLng&lpar;x0&lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt; &lt;span class=&quot;hljs-operator&quot;&gt;-&lt;/span&gt; &lt;span class=&quot;hljs-number&quot;&gt;0&lt;/span&gt;&lt;span class=&quot;hljs-number&quot;&gt;.5&lt;/span&gt;, y0&lt;span class=&quot;hljs-operator&quot;&gt;!&lt;/span&gt; &lt;span class=&quot;hljs-operator&quot;&gt;-&lt;/span&gt; &lt;span class=&quot;hljs-number&quot;&gt;0&lt;/span&gt;&lt;span class=&quot;hljs-number&quot;&gt;.5&lt;/span&gt;&rpar;&rpar;;
  }
}
&lt;/code&gt;&lt;/pre&gt;&lt;p&gt;Now we can update our &lt;strong&gt;GoogleMap&lt;/strong&gt; widget to add the markers and &lt;strong&gt;polyline parameters&lt;/strong&gt;. &lt;/p&gt;
&lt;pre&gt;&lt;code&gt;&lt;span class=&quot;hljs-string&quot;&gt;GoogleMap&lpar;&lt;/span&gt;
  &lt;span class=&quot;hljs-attr&quot;&gt;onMapCreated:&lt;/span&gt; &lt;span class=&quot;hljs-string&quot;&gt;&lpar;GoogleMapController&lt;/span&gt; &lt;span class=&quot;hljs-string&quot;&gt;controller&rpar;&lt;/span&gt; {
    &lt;span class=&quot;hljs-string&quot;&gt;_controllerGoogleMap.complete&lpar;controller&rpar;;&lt;/span&gt;
    &lt;span class=&quot;hljs-string&quot;&gt;_googleMapController&lt;/span&gt; &lt;span class=&quot;hljs-string&quot;&gt;=&lt;/span&gt; &lt;span class=&quot;hljs-string&quot;&gt;controller;&lt;/span&gt;
  }&lt;span class=&quot;hljs-string&quot;&gt;,&lt;/span&gt;
  &lt;span class=&quot;hljs-attr&quot;&gt;initialCameraPosition:&lt;/span&gt; &lt;span class=&quot;hljs-string&quot;&gt;const&lt;/span&gt; &lt;span class=&quot;hljs-string&quot;&gt;CameraPosition&lpar;&lt;/span&gt;
    &lt;span class=&quot;hljs-attr&quot;&gt;target:&lt;/span&gt; &lt;span class=&quot;hljs-string&quot;&gt;_center,&lt;/span&gt;
    &lt;span class=&quot;hljs-attr&quot;&gt;zoom:&lt;/span&gt; &lt;span class=&quot;hljs-number&quot;&gt;11.0&lt;/span&gt;&lt;span class=&quot;hljs-string&quot;&gt;,&lt;/span&gt;
  &lt;span class=&quot;hljs-string&quot;&gt;&rpar;,&lt;/span&gt;
  &lt;span class=&quot;hljs-attr&quot;&gt;markers:&lt;/span&gt; {
    &lt;span class=&quot;hljs-string&quot;&gt;if&lt;/span&gt; &lt;span class=&quot;hljs-string&quot;&gt;&lpar;_origin&lt;/span&gt; &lt;span class=&quot;hljs-type&quot;&gt;!=&lt;/span&gt; &lt;span class=&quot;hljs-literal&quot;&gt;null&lt;/span&gt;&lt;span class=&quot;hljs-string&quot;&gt;&rpar;&lt;/span&gt; &lt;span class=&quot;hljs-string&quot;&gt;_origin!&lt;/span&gt;,
    &lt;span class=&quot;hljs-string&quot;&gt;if&lt;/span&gt; &lt;span class=&quot;hljs-string&quot;&gt;&lpar;_destination&lt;/span&gt; &lt;span class=&quot;hljs-type&quot;&gt;!=&lt;/span&gt; &lt;span class=&quot;hljs-literal&quot;&gt;null&lt;/span&gt;&lt;span class=&quot;hljs-string&quot;&gt;&rpar;&lt;/span&gt; &lt;span class=&quot;hljs-string&quot;&gt;_destination!&lt;/span&gt;
  }&lt;span class=&quot;hljs-string&quot;&gt;,&lt;/span&gt;
  &lt;span class=&quot;hljs-attr&quot;&gt;polylines:&lt;/span&gt; {&lt;span class=&quot;hljs-string&quot;&gt;if&lt;/span&gt; &lt;span class=&quot;hljs-string&quot;&gt;&lpar;polylineValues.isNotEmpty&rpar;&lt;/span&gt; &lt;span class=&quot;hljs-string&quot;&gt;polylineValues&lt;/span&gt;[&lt;span class=&quot;hljs-number&quot;&gt;0&lt;/span&gt;]}&lt;span class=&quot;hljs-string&quot;&gt;,&lt;/span&gt;
&lt;span class=&quot;hljs-string&quot;&gt;&rpar;,&lt;/span&gt;
&lt;/code&gt;&lt;/pre&gt;&lt;p&gt;Now, let&#39;s run the app again and see how is our app performing.&lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1654242450481/pbqruybSK.gif&quot; alt=&quot;ezgif.com-gif-maker.gif&quot; /&gt;&lt;/p&gt;
&lt;p&gt;Our app is work is working perfectly!!&lt;/p&gt;
&lt;h1 id=&quot;heading-conclusion&quot;&gt;Conclusion&lt;/h1&gt;
&lt;p&gt;You can now easily add a simple map feature to any of your apps very simply on a single page. The code might seem to be long but it will provide all the necessary functions and features for the user and the app. You can also add more functionality and features using the markers and PolyLines for your use case. 
If you are reading this. Thank you for reading my blog, I hope it helped and clarified all the doubts regarding the topic.&lt;/p&gt;
&lt;h1 id=&quot;heading-github-link&quot;&gt;GitHub Link&lt;/h1&gt;
&lt;p&gt;You can also check out the whole project on my &lt;a target=&quot;_blank&quot; href=&quot;https://github.com/achintya-7/maps_demo&quot;&gt;GitHub&lt;/a&gt;.&lt;/p&gt;
## 
 - 🚀 [KubeSphere 101](https://achintya-7.hashnode.dev/kubesphere-101) - &lt;h1 id=&quot;heading-what-is-kubesphere&quot;&gt;What is KubeSphere?&lt;/h1&gt;
&lt;p&gt;KubeSphere is a distributed operating system for cloud-native application management, using Kubernetes as its kernel. It provides a plug-and-play architecture, allowing third-party applications to be seamlessly integrated into its ecosystem. It is also Open Source certified by CNCF. &lt;/p&gt;
&lt;p&gt;To get a good view and experience of UI. You can run a demo version of KubeSphere in your browser from &lt;a target=&quot;_blank&quot; href=&quot;https://demo.kubesphere.io/login&quot;&gt;here&lt;/a&gt;. &lt;/p&gt;
&lt;h1 id=&quot;heading-why-kubesphere&quot;&gt;Why KubeSphere?&lt;/h1&gt;
&lt;p&gt;KubeSphere provides high-performance and scalable container service management for enterprises. It aims to help them accomplish digital transformation driven by cutting-edge technologies, and accelerate app iteration and business delivery to meet the ever-changing needs of enterprises.&lt;/p&gt;
&lt;h1 id=&quot;heading-key-features&quot;&gt;Key Features&lt;/h1&gt;
&lt;ul&gt;
&lt;li&gt;&lt;h3 id=&quot;heading-provisioning-kubernetes&quot;&gt;Provisioning Kubernetes&lt;/h3&gt;
&lt;p&gt;Deploy Kubernetes anywhere easily. It also includes online and air-gapped installation, and supports for adding GPU nodes. &lt;/p&gt;
&lt;/li&gt;
&lt;li&gt;&lt;h3 id=&quot;heading-k8s-resource-management&quot;&gt;K8s Resource Management&lt;/h3&gt;
&lt;p&gt;  A web console for creating and managing Kubernetes resources with powerful 
  observability&lt;/p&gt;
&lt;/li&gt;
&lt;li&gt;&lt;h3 id=&quot;heading-multi-tenant-management&quot;&gt;Multi-tenant Management&lt;/h3&gt;
&lt;p&gt;  Provide unified authentication with fine-grained roles and a three-tier authorization system, and support AD/LDAP authentication&lt;/p&gt;
&lt;/li&gt;
&lt;li&gt;&lt;h3 id=&quot;heading-multiple-storage-and-networking-solutions&quot;&gt;Multiple Storage and Networking Solutions&lt;/h3&gt;
&lt;p&gt; Multiple Storage and Networking Solutions
Support GlusterFS, CephRBD, NFS, LocalPV solutions, and provide CSI plugins to consume storage from multiple cloud providers.&lt;/p&gt;
&lt;/li&gt;
&lt;/ul&gt;
&lt;h1 id=&quot;heading-kubesphere-ecosystem-tools&quot;&gt;KubeSphere Ecosystem Tools&lt;/h1&gt;
&lt;p&gt;KubeSphere integrate a large variety of tools related to Kubernetes, ranging from cloud-native apps to the underlying container runtimes. These open-source projects serve as the backend components of KubeSphere, which interact with the KubeSphere console through standard APIs, thus providing consistent user experiences to reduce complexity. &lt;br /&gt;
Various open-source tools like GitLab&#39;s, Ceph, Mongo-DB, etc. can be easily used by leveraging the functionality of KubeSphere 
&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1653230271056/DwIGlsRnn.png&quot; alt=&quot;image.png&quot; /&gt;&lt;/p&gt;
&lt;h1 id=&quot;heading-use-cases&quot;&gt;Use Cases&lt;/h1&gt;
&lt;p&gt;KubeSphere is applicable in a variety of scenarios. For enterprises that deploy their business system on bare metal, their business modules are tightly coupled with each other. That means it is extremely difficult for resources to be horizontally scaled. In this connection, KubeSphere provides enterprises with containerized environments with a complete set of features for management and operation. It empowers enterprises to rise to the challenges in the middle of their digital transformation, including agile software development, automated operation and maintenance, microservices governance, traffic management, autoscaling, high availability, as well as DevOps and CI/CD.&lt;/p&gt;
&lt;ul&gt;
&lt;li&gt;&lt;h3 id=&quot;heading-multi-cluster-deployment&quot;&gt;Multi-cluster Deployment&lt;/h3&gt;
&lt;ul&gt;
&lt;li&gt;&lt;strong&gt;High Availability &lt;/strong&gt; &lt;br /&gt;
 Users can deploy workloads on multiple clusters by using a global VIP or DNS to 
 send requests to corresponding backend clusters.&lt;/li&gt;
&lt;li&gt;&lt;strong&gt;Low Latency&lt;/strong&gt; &lt;br /&gt;
 When clusters are deployed in various regions, user requests can be forwarded to 
 the nearest cluster, greatly reducing network latency.&lt;/li&gt;
&lt;li&gt;&lt;strong&gt;Avoid Vendor Lock-in&lt;/strong&gt; &lt;br /&gt;
 Kubernetes has become the de-facto standard in container orchestration. Against 
 this backdrop, many enterprises avoid putting all eggs in one basket as they deploy 
 clusters by using services of different cloud providers. &lt;/li&gt;
&lt;/ul&gt;
&lt;/li&gt;
&lt;li&gt;&lt;h3 id=&quot;heading-full-stack-observability-with-streamlined-oandampm&quot;&gt;Full-stack Observability with Streamlined O&amp;amp;M&lt;/h3&gt;
&lt;ul&gt;
&lt;li&gt;&lt;strong&gt;Multi-dimensional Cluster Monitoring&lt;/strong&gt; &lt;br /&gt;
 The adoption of multi-cluster deployment across clouds is on the rise both among 
 individuals and enterprises.&lt;/li&gt;
&lt;li&gt;&lt;strong&gt;Log Query&lt;/strong&gt; &lt;br /&gt;
 A comprehensive monitoring feature is meaningless without a flexible log query 
 system. This is because users need to be able to track all the information related to 
 their resources, such as alerting messages, node scheduling status, app deployment 
 success, or network policy modification. &lt;/li&gt;
&lt;li&gt;&lt;strong&gt;Customization&lt;/strong&gt; &lt;br /&gt;
 Even for resource monitoring on the same platform, the tool provided by the cloud 
 vendor may not be a panacea. In some cases, users need to create their own 
 standard of observability, such as the specific monitoring metrics and display form.&lt;/li&gt;
&lt;/ul&gt;
&lt;/li&gt;
&lt;li&gt;&lt;h3 id=&quot;heading-implement-devops-practices&quot;&gt;Implement DevOps Practices&lt;/h3&gt;
&lt;p&gt;  DevOps represents an important set of practices or methods that engage both 
  development and Ops teams for more coordinated and efficient cooperation between 
  them. Therefore, development, testing and release can be faster, more efficient and 
  more reliable. CI/CD pipelines in KubeSphere provide enterprises with agile 
  development and automated O&amp;amp;M. &lt;/p&gt;
&lt;/li&gt;
&lt;li&gt;&lt;h3 id=&quot;heading-service-mesh-and-cloud-native-architecture&quot;&gt;Service Mesh and Cloud-native Architecture&lt;/h3&gt;
&lt;ul&gt;
&lt;li&gt;&lt;p&gt;&lt;strong&gt;Multi-cloud App Distribution&lt;/strong&gt; &lt;br /&gt;
As mentioned above, it is not uncommon for individuals or organizations to deploy 
apps across Kubernetes clusters, whether on-premises, public or hybrid. &lt;/p&gt;
&lt;/li&gt;
&lt;li&gt;&lt;p&gt;&lt;strong&gt;Visualization&lt;/strong&gt; &lt;br /&gt;
As users deploy microservices which will communicate among themselves 
considerably, it will help users gain a better understanding of topological relations 
between microservices, if the connection is highly visualized.&lt;/p&gt;
&lt;/li&gt;
&lt;/ul&gt;
&lt;/li&gt;
&lt;li&gt;&lt;h3 id=&quot;heading-bare-metal-deployment&quot;&gt;Bare Metal Deployment&lt;/h3&gt;
&lt;p&gt; Sometimes, the cloud is not necessarily the ideal place for the deployment of 
 resources. For example, physical, dedicated servers tend to function better when it 
 comes to cases that require considerable computing resources and high disk I/O. 
 Besides, for some specialized workloads that are difficult to migrate to a cloud 
 environment, certified hardware and complicated licensing and support agreements 
 may be required.&lt;/p&gt;
&lt;/li&gt;
&lt;/ul&gt;
&lt;h1 id=&quot;heading-installation&quot;&gt;Installation&lt;/h1&gt;
&lt;h3 id=&quot;heading-prerequisites&quot;&gt;Prerequisites&lt;/h3&gt;
&lt;ul&gt;
&lt;li&gt;Kubernetes version v1.19.x, v1.20.x, v1.21.x, or v1.22.x &lpar;experimental&rpar;.&lt;/li&gt;
&lt;li&gt;CPU Cores &amp;gt; 1 &amp;amp;&amp;amp; Ram &amp;gt; 2GB. {Only working on x86_64 CPUs for now}.&lt;/li&gt;
&lt;li&gt;A default StorageClass in your Kubernetes cluster, use &lt;code&gt;kubectl get sc&lt;/code&gt; to verify it.&lt;/li&gt;
&lt;/ul&gt;
&lt;h3 id=&quot;heading-installation&quot;&gt;Installation&lt;/h3&gt;
&lt;p&gt;If you meet all the previous prerequisites, you can install KubeSphere with these commands.&lt;/p&gt;
&lt;pre&gt;&lt;code&gt;&lt;span class=&quot;hljs-attribute&quot;&gt;kubectl&lt;/span&gt; apply -f https://github.com/kubesphere/ks-installer/releases/download/v&lt;span class=&quot;hljs-number&quot;&gt;3&lt;/span&gt;.&lt;span class=&quot;hljs-number&quot;&gt;2&lt;/span&gt;.&lt;span class=&quot;hljs-number&quot;&gt;1&lt;/span&gt;/kubesphere-installer.yaml

&lt;span class=&quot;hljs-attribute&quot;&gt;kubectl&lt;/span&gt; apply -f https://github.com/kubesphere/ks-installer/releases/download/v&lt;span class=&quot;hljs-number&quot;&gt;3&lt;/span&gt;.&lt;span class=&quot;hljs-number&quot;&gt;2&lt;/span&gt;.&lt;span class=&quot;hljs-number&quot;&gt;1&lt;/span&gt;/cluster-configuration.yaml
&lt;/code&gt;&lt;/pre&gt;&lt;p&gt;You can check the logs while the installation is going on. Use this command to check the logs &lt;/p&gt;
&lt;pre&gt;&lt;code&gt;kubectl logs &lt;span class=&quot;hljs-operator&quot;&gt;-&lt;/span&gt;n kubesphere&lt;span class=&quot;hljs-operator&quot;&gt;-&lt;/span&gt;system $descriptionlpar;kubectl get pod &lt;span class=&quot;hljs-operator&quot;&gt;-&lt;/span&gt;n kubesphere&lt;span class=&quot;hljs-operator&quot;&gt;-&lt;/span&gt;system &lt;span class=&quot;hljs-operator&quot;&gt;-&lt;/span&gt;l app&lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt;ks&lt;span class=&quot;hljs-operator&quot;&gt;-&lt;/span&gt;install &lt;span class=&quot;hljs-operator&quot;&gt;-&lt;/span&gt;o jsonpath&lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt;&lt;span class=&quot;hljs-string&quot;&gt;&#39;{.items[0].metadata.name}&#39;&lt;/span&gt;&rpar; &lt;span class=&quot;hljs-operator&quot;&gt;-&lt;/span&gt;f
&lt;/code&gt;&lt;/pre&gt;&lt;p&gt;Use this command to check if all the ports are working properly&lt;/p&gt;
&lt;pre&gt;&lt;code&gt;kubectl get svc&lt;span class=&quot;hljs-operator&quot;&gt;/&lt;/span&gt;ks&lt;span class=&quot;hljs-operator&quot;&gt;-&lt;/span&gt;console &lt;span class=&quot;hljs-operator&quot;&gt;-&lt;/span&gt;n kubesphere&lt;span class=&quot;hljs-operator&quot;&gt;-&lt;/span&gt;system
&lt;/code&gt;&lt;/pre&gt;&lt;p&gt;go to localhost port 30880 to start using KubeSphere
the default credentials are following&lt;/p&gt;
&lt;blockquote&gt;
&lt;p&gt;Admin : admin &lt;/p&gt;&lt;p&gt;
Password : P@88w0rd&lt;/p&gt;
&lt;/blockquote&gt;
&lt;p&gt;If you want to install KubeSphere on the cloud, you can check their docs &lt;a target=&quot;_blank&quot; href=&quot;https://kubesphere.io/docs/installing-on-kubernetes/hosted-kubernetes/install-kubesphere-on-aks/&quot;&gt;here&lt;/a&gt;&lt;/p&gt;
&lt;h1 id=&quot;heading-conclusion&quot;&gt;Conclusion&lt;/h1&gt;
&lt;p&gt;This was a basic synopsis of KubeSphere and all the services it provides. You can also check out their website to know more about &lt;a target=&quot;_blank&quot; href=&quot;https://kubesphere.io&quot;&gt;KubeSphere&lt;/a&gt;.&lt;/p&gt;
## 
 - 💯 [Portainer 101](https://achintya-7.hashnode.dev/portainer-101) - &lt;h1 id=&quot;heading-what-is-portainer&quot;&gt;What is Portainer?&lt;/h1&gt;
&lt;ul&gt;
&lt;li&gt;Portainer is one of the most popular container management platforms. &lt;/li&gt;
&lt;li&gt;It can be deployed anywhere, be it cloud, local machine or hybrid and gives user visibility across multiple container environments through a single interface.&lt;/li&gt;
&lt;/ul&gt;
&lt;h1 id=&quot;heading-features-of-portainer&quot;&gt;Features of Portainer&lt;/h1&gt;
&lt;ul&gt;
&lt;li&gt;&lt;strong&gt;Application Deployment&lt;/strong&gt; - It provides a clean GUI for managing, deploying and automating the deployment process.&lt;/li&gt;
&lt;li&gt;&lt;strong&gt;Observability &amp;amp; Triage&lt;/strong&gt; - Monitor the performance and behaviour of containerized applications&lt;/li&gt;
&lt;li&gt;&lt;strong&gt;Centralized IAM&lt;/strong&gt; - Assign who can do what with the team and roles&lt;/li&gt;
&lt;li&gt;&lt;strong&gt;Platform Management&lt;/strong&gt; - Set up and configure your environment - on-prem, in the cloud or at the edge.&lt;/li&gt;
&lt;/ul&gt;
&lt;h1 id=&quot;heading-installing-portainer&quot;&gt;Installing Portainer&lt;/h1&gt;
&lt;p&gt;You must have docker or docker desktop on your machine pr server to install Portainer via docker. You can check about installing docker from &lt;a target=&quot;_blank&quot; href=&quot;https://docs.docker.com/get-docker/&quot;&gt;here&lt;/a&gt;.&lt;/p&gt;
&lt;p&gt;If you have Docker Desktop, you can install it directly via the extension tab. We will use the terminal to install it. I am using WSL2 for Windows here to install it.&lt;/p&gt;
&lt;ul&gt;
&lt;li&gt;First, we need to make a volume for Portainer Server to store its database. &lt;/li&gt;
&lt;/ul&gt;
&lt;pre&gt;&lt;code&gt;docker volume &lt;span class=&quot;hljs-keyword&quot;&gt;create&lt;/span&gt; portainer_data
&lt;/code&gt;&lt;/pre&gt;&lt;ul&gt;
&lt;li&gt;Now, we have to download and install Portainer&lt;/li&gt;
&lt;/ul&gt;
&lt;pre&gt;&lt;code&gt;docker run &lt;span class=&quot;hljs-operator&quot;&gt;-&lt;/span&gt;d &lt;span class=&quot;hljs-operator&quot;&gt;-&lt;/span&gt;p &lt;span class=&quot;hljs-number&quot;&gt;8000&lt;/span&gt;:&lt;span class=&quot;hljs-number&quot;&gt;8000&lt;/span&gt; &lt;span class=&quot;hljs-operator&quot;&gt;-&lt;/span&gt;p &lt;span class=&quot;hljs-number&quot;&gt;9443&lt;/span&gt;:&lt;span class=&quot;hljs-number&quot;&gt;9443&lt;/span&gt; &lt;span class=&quot;hljs-operator&quot;&gt;-&lt;/span&gt;&lt;span class=&quot;hljs-operator&quot;&gt;-&lt;/span&gt;name portainer &lt;span class=&quot;hljs-operator&quot;&gt;-&lt;/span&gt;&lt;span class=&quot;hljs-operator&quot;&gt;-&lt;/span&gt;restart&lt;span class=&quot;hljs-operator&quot;&gt;=&lt;/span&gt;always &lt;span class=&quot;hljs-operator&quot;&gt;-&lt;/span&gt;v &lt;span class=&quot;hljs-operator&quot;&gt;/&lt;/span&gt;&lt;span class=&quot;hljs-keyword&quot;&gt;var&lt;/span&gt;&lt;span class=&quot;hljs-operator&quot;&gt;/&lt;/span&gt;run&lt;span class=&quot;hljs-operator&quot;&gt;/&lt;/span&gt;docker.sock:&lt;span class=&quot;hljs-operator&quot;&gt;/&lt;/span&gt;&lt;span class=&quot;hljs-keyword&quot;&gt;var&lt;/span&gt;&lt;span class=&quot;hljs-operator&quot;&gt;/&lt;/span&gt;run&lt;span class=&quot;hljs-operator&quot;&gt;/&lt;/span&gt;docker.sock &lt;span class=&quot;hljs-operator&quot;&gt;-&lt;/span&gt;v portainer_data:&lt;span class=&quot;hljs-operator&quot;&gt;/&lt;/span&gt;data portainer&lt;span class=&quot;hljs-operator&quot;&gt;/&lt;/span&gt;portainer&lt;span class=&quot;hljs-operator&quot;&gt;-&lt;/span&gt;ce:&lt;span class=&quot;hljs-number&quot;&gt;2.9&lt;/span&gt;&lt;span class=&quot;hljs-number&quot;&gt;.3&lt;/span&gt;
&lt;/code&gt;&lt;/pre&gt;&lt;ul&gt;
&lt;li&gt;You can now go to your localhost on port 9443 to start using Portainer&lt;/li&gt;
&lt;/ul&gt;
&lt;pre&gt;&lt;code&gt;&lt;span class=&quot;hljs-attribute&quot;&gt;https&lt;/span&gt;:&lt;span class=&quot;hljs-comment&quot;&gt;//localhost:9443&lt;/span&gt;
&lt;/code&gt;&lt;/pre&gt;&lt;p&gt;Now you can sign up and will be introduced to the home page of Portainer.&lt;/p&gt;
&lt;h1 id=&quot;heading-making-a-new-container&quot;&gt;Making a new Container&lt;/h1&gt;
&lt;p&gt;You can now go to the dashboard to see your local machine and can get a good brief status of your local docker environment.&lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1652534274292/P8KUNOwAR.png&quot; alt=&quot;image.png&quot; /&gt;&lt;/p&gt;
&lt;p&gt;Let&#39;s click on it and explore&lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1652534871687/8OV2RZdxb.png&quot; alt=&quot;image.png&quot; /&gt;&lt;/p&gt;
&lt;p&gt;We see a clean UI and get information on all the resources or local docker environment is using. Let&#39;s try adding a new docker image from the docker hub.  Let&#39;s now make a new container and install Nginx in it. 
Go to container and press add a container.&lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1652537534385/05LqPYAqP.png&quot; alt=&quot;image.png&quot; /&gt;&lt;/p&gt;
&lt;p&gt;You can fill in the information like name and port with whatever parameters you like or you can follow my configurations. You can also search all images by using the image search field as well. For this blog&#39;s purpose, let&#39;s install Nginx.&lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1652538037675/SUwsTx_yp.png&quot; alt=&quot;image.png&quot; /&gt;&lt;/p&gt;
&lt;p&gt;Click on &lt;strong&gt;Deploy the Container&lt;/strong&gt; and voila! Your container is created and running after the loading. 
You can now click that container and get all the information about it.&lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1652538244087/1J4x4qEHu.png&quot; alt=&quot;image.png&quot; /&gt;&lt;/p&gt;
&lt;p&gt;You can now go to the mentioned port and start using Nginx.&lt;/p&gt;
&lt;h1 id=&quot;heading-iam-features&quot;&gt;IAM Features&lt;/h1&gt;
&lt;p&gt;Let&#39;s look at the IAM features in Portainer. 
In portainer, you can add other users and assign roles to them as well. A very necessary feature for organizations very easily implemented from here. In Setting go to user and add a new user.  &lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1652538619467/upcWcgjdT.png&quot; alt=&quot;image.png&quot; /&gt;&lt;/p&gt;
&lt;p&gt;After adding the information, click &lt;strong&gt;Create user&lt;/strong&gt;. On the free tier of Portainer, only standard role can be assigned to a user. You now have to give this user access to any of the environments being maintained by the portainer. 
Go to &lt;strong&gt;Environments&lt;/strong&gt; in the sub-menu and select &lt;strong&gt;Manage Access&lt;/strong&gt;.  &lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1652539189565/0xZm4DAuO.png&quot; alt=&quot;image.png&quot; /&gt;&lt;/p&gt;
&lt;p&gt;You can now select the user and assign his/her role.&lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1652539286528/2-H7WlwMk.png&quot; alt=&quot;image.png&quot; /&gt;&lt;/p&gt;
&lt;p&gt;Just click &lt;strong&gt;Create Access&lt;/strong&gt; and a new user is now assigned. 
Let&#39;s log out and sign in from the new user. You can log out by clicking on the top right button.&lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1652539563605/m3m67vHTG.png&quot; alt=&quot;image.png&quot; /&gt;&lt;/p&gt;
&lt;p&gt;As you can see, the non-administrative new user doesn&#39;t have access to other containers but can make his new containers. This also applies to other aspects like volumes and images. &lt;/p&gt;
&lt;p&gt;Let&#39;s create a new container by using App Template.
Go to App Template in the sub-menu and select a container template you want to start. I am going to install a node.js server. Click on it and fill in the parameters.&lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1652540378913/QdyOkX51E.png&quot; alt=&quot;image.png&quot; /&gt;&lt;/p&gt;
&lt;p&gt;Just click &lt;strong&gt;&lt;em&gt;Deploy the Container&lt;/em&gt;&lt;/strong&gt; and now we have a node.js server.&lt;/p&gt;
&lt;p&gt;Let&#39;s re-login to our main account and we can see that there are 3 containers now. I being an admin can manage all 3 of them. &lt;/p&gt;
&lt;p&gt;&lt;img src=&quot;https://cdn.hashnode.com/res/hashnode/image/upload/v1652540957877/EpxKwFQYJ.png&quot; alt=&quot;image.png&quot; /&gt;&lt;/p&gt;
&lt;h1 id=&quot;heading-conclusion&quot;&gt;Conclusion&lt;/h1&gt;
&lt;p&gt;I have provided some basic use cases and examples of using Portainer like making Containers and assigning Roles. You can do much more with Portainer like writing custom templates and adding more environments. You can also look at their official documentation &lt;a target=&quot;_blank&quot; href=&quot;https://docs.portainer.io&quot;&gt;here&lt;/a&gt;.&lt;/p&gt;
&lt;p&gt;If you&#39;ve reached so far thanks for reading. Hopefully, this blog has helped you get a better understanding of how to use portainer.&lt;/p&gt;
<!-- BLOGPOSTS:END -->

# Technologies

### Language :
![Python](https://img.shields.io/badge/-Python-black?style=flat-square&logo=Python)
![Java](https://img.shields.io/badge/-java-darkblue?style=flat-square&logo=java)
![Kotlin](https://img.shields.io/badge/-Kotlin-black?style=flat-square&logo=Kotlin)
![Dart](https://img.shields.io/badge/-Dart-blue?style=flat-square&logo=Dart)
![C++](https://img.shields.io/badge/-C++-00599C?style=flat-square&logo=c)
![MySQL](https://img.shields.io/badge/-MySQL-black?style=flat-square&logo=mysql)


### Libraries & Framework :

![Flutter](https://img.shields.io/badge/-Flutter-blue?style=flat-square&logo=Flutter)
![Tensorflow](https://img.shields.io/badge/-Tensorflow-white?style=flat-square&logo=tensorflow)
![ElasticSearch](https://img.shields.io/badge/-ElasticSearch-005571?style=flat-square&logo=elasticsearch)
![VelocityX](https://img.shields.io/badge/-VelocityX-E10098?style=flat-square&logo=VelocityX)
![Google Cloud](https://img.shields.io/badge/Google%20Cloud-black?style=flat-square&logo=google-cloud)
![Docker](https://img.shields.io/badge/-Docker-black?style=flat-square&logo=docker)
![Appwrite](https://img.shields.io/badge/-Appwrite-white?style=flat-square&logo=Appwrite)
![Git](https://img.shields.io/badge/-Git-black?style=flat-square&logo=git)
<a href="#"><img alt="Keras" src="https://img.shields.io/badge/Keras%20-%23D00000.svg?logo=Keras&logoColor=white"></a>
<a href="#"><img alt="Material Design" src="https://img.shields.io/badge/Material%20Design%20-%230081CB.svg?logo=material-design&logoColor=white"></a>
<a href="#"><img alt="NumPy" src="https://img.shields.io/badge/Numpy%20-%23013243.svg?logo=numpy&logoColor=white"></a>
<a href="#"><img alt="Pandas" src="https://img.shields.io/badge/Pandas%20-%23150458.svg?logo=pandas&logoColor=white"></a>

# 📈 Stats
<p align="center">
	
  <img width="48%" src="https://github-readme-stats.vercel.app/api?username=achintya-7&show_icons=true&theme=tokyonight" />
  <img width="48%" src="https://github-readme-streak-stats.herokuapp.com/?user=achintya-7&theme=tokyonight" />
</p>

# :musical_note: Recent Jams
[![spotify-github-profile](https://spotify-github-profile.vercel.app/api/view?uid=22rwq3xgfxaeiogrerlrhqwjy&cover_image=true&theme=novatorem&bar_color=53b14f&bar_color_cover=false)](https://spotify-github-profile.vercel.app/api/view?uid=22rwq3xgfxaeiogrerlrhqwjy&redirect=true)



