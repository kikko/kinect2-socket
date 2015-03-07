# kinect-socket module

_kinect-socket is a little x64 windows desktop application that streams KinectV2 body tracking datas using websocket and a simple JSON protocol_

![Screenshot](https://bitbucket.org/field/139-sap-x-livenation/raw/feature-kinect-socket/production/apps/mirror/modules/kinect-socket/res/screen.png)

## features :

current :

	* skeleton tracking data streaming for up to 6 people at ~30hz
	* 25 joints per person
	* hand states
    * 3D and 2D debug views
    * ground plane detection

to be implemented :

    * send skeleton position relative to ground plane
    * gesture detection :
        - jump
        - hand raised
        - hand wave
        - arms flap
        - claps
    * feature detection :
        - size
        - clothes colors
    * audio detection

## protocol

kinect datas are streamed via websocket at ~30hz on port 9092

```
    {
        bodies : [
            {
        	"id" : int             // tracking id
        	"leftHandState" : int  // left hand state (unknown|nottracked|open|closed|lasso)
        	"rightHandState" : int // right hand state (unknown|nottracked|open|closed|lasso)
            "joints" : [            // array of joints positions {x,y,z}
                {
                    "x" : float
                    "y" : float
                    "z" : float
                },
                ...
            ]
            },
            ...
        ]
    }
```

how to receive datas (coffeescript example) :
```
 socket = new WebSocket 'ws://localhost:9092'
 socket.onmessage = (msg) =>
    console.log Json.parse(msg.data)
```

## compilation

Setting up compilation for this module is fairly complicated for now as it's using a few experimental libraries forks (VS2013 64bits OF, custom ofxKinectForWindows2, custom ofxLibwebsockets) so you're greatly encouraged to use the latest release binary instead.

In order to compile, the OF and extras addons paths must be added to visual studio properties :

![Screenshot](https://bitbucket.org/field/139-sap-x-livenation/raw/feature-kinect-socket/production/apps/mirror/modules/kinect-socket/res/p1.png)

![Screenshot](https://bitbucket.org/field/139-sap-x-livenation/raw/feature-kinect-socket/production/apps/mirror/modules/kinect-socket/res/p2.png)