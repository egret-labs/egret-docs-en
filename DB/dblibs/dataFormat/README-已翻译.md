## 4.5 Data Format Standard Description
```javascript
{
    // DragonBones data name
    "name": "dragonBonesName",

    // data version
    "version": "4.5",

    // Animation frame rate
    "frameRate": 24,

    // Whether use absolute data or not [0: use relative date; 1: use absolute data] (optional properties, default value: 1)
    "isGlobal": 1,

    // Skeleton list
    "armature": [{

        // Skeleton name (one DragonBones data could contain multiple skeletons)
        "name": "armatureName",

        // Animation frame rate (optional properties: use global frame rate by default)
        "frameRate": 24,

        // Animation type (optional properties, “Armature by default”)
        // ["Armature": Skeleton animation, "MovieClip": basic animation, "Stage": stage animation]
        "type": "Armature",

        // Custom data [any type] (optional properties, null by default)
        "userData": null,

        // Behavior list by default that’s added to the stage (optional properties, null by default)
        "defaultActions": [

            // This skeleton plays specified animation
            ["gotoAndPlay", "animationName"],

            // This skeleton plays and stops specified animation 
            ["gotoAndStop", "animationName"],
        ],

        // bone list of this skeleton contains
        "bone": [{

            // bone name
            "name": "boneName",

            // 父Parent bone name
            "parent": "parentBoneName",

            // Custom data [any type] (optional properties, null by default)
            "userData": null,

            // Bone’s registration to skeleton: replacement/chamfer/zoom (optional properties, null by default)
            "transform": {
                "x": 0.00, // Horizontal displacement (Optional properties, 0.00 by defalut)
                "y": 0.00, // Vertical displacement (optional properties, 0.00 by defalut)
                "skX": 0.0000, // Horizontal chamfer (optional properties, 0.0000 by default)
                "skY": 0.0000, // Vertical chamfer (optional properties  0.0000 by default)
                "scX": 1.0000, // horizontal zoom (optional properties, 1.0000 by default)
                "scY": 1.0000, // Vertical zoom (optional properties, 1.0000 by default)
            }
        }],

        // Slot list of this skeleton
        "slot": [{

            // slot name
            "name": "slotName",

            // Parent bone name of the slot
            "parent": "parentBoneName",

            // Index of display object by default (optional properties, 0 by default)
            "displayIndex": 0,

            // Blend mode (optional properties, null by default)
            "blendMode": null,

            // Custom data [any type] (optional properties, null by default)
            "userData": null,

            // Color overlay of display object (Optional properties, null by default)
            "color": {
                "aM": 100, //  Transparent overlay [0~100] (Optional properties default: 100)
                "rM": 100, // red overlay [0~100] (Optional properties default: 100)
                "gM": 100, // green overlay [0~100] (Optional properties default: 100)
                "bM": 100, // blue overlay [0~100] (Optional properties default: 100)
                "aO": 0.00, // Transparent skew [-255~255] (Optional properties default: 0)
                "rO": 0.00, // red skew [-255~255] (Optional properties default: 0)
                "gO": 0.00, // green skew [-255~255] (Optional properties default: 0)
                "bO": 0.00, // blue skew [-255~255] (Optional properties default: 0)
            },

            // Behavior list that’s added to the stage (optional properties, null by default)
            "actions": [

                // Child skeleton play specified animation (only available when display object is skeleton)
                ["gotoAndPlay", "animationName"],

                // Child skeleton play and stop specified animation (only available when display object is skeleton)
                ["gotoAndStop", "animationName"],
            ]
        }],

        // Skin list of this skeleton contains
        "skin": [{

            // skin name
            "name": "skinName",

            // Slot list of this skin contains
            "slot": [{

                // slot name
                "name": "slotName",

                // Display object list of this slot contains
                "display": [{

                    // Display object name
                    "name": "displayName",

                    // Display object type (Optional properties, image by default)
                    // ["image": chartlet, "armature": skeleton, "mesh": mesh, ... Other extension types]
                    "type": "image",

                    // Display object displacement/chamfer/zoom relative to bone (optional properties default: null)
                    "transform": {
                        "x": 0.00, // horizontal displacement (Optional properties, 0.00 by default)
                        "y": 0.00, // y vertical displacement (Optional properties, 0.00 by default)
                        "skX": 0.0000, // Horizontal chamfer (Optional properties, 0.0000 by default)
                        "skY": 0.0000, // Vertical chamfer (Optional properties, 0.0000 by default)
                        "scX": 1.0000, // Vertical zoom (optional properties, 1.0000 by default)
                        "scY": 1.0000, // Vertical zoom (optional properties, 1.0000 by default)
                    },

                    // Pivot point of display object (Optional properties, null by default, only available to textures or grids)
                    "pivot": {
                        "x": 0.50, // horizontal pivot point [0.00~1.00] (Optional properties, 0.50 by default)
                        "y": 0.50, // vertical pivot point [0.00~1.00] (Optional properties, 0.50 by default)
                    },

                    // Vertex UV coordinate list (Optional properties, null by default, only available to mesh)
                    // [u0, v0, u1, v1, ...]
                    "uvs": [0.0000, 0.0000, 1.0000, 0.0000, 1.0000, 1.0000, 0.0000, 1.0000],

                    // Triangle vertex index list (Optional properties, null by default, only available to mesh) 
                    "triangles": [0, 1, 2, 2, 3, 0],

                    // Vertex weight list (Optional properties, null by default, only available to mesh)
                    // [Vertex index, bone index, weight, ...]
                    "weights": [0, 0, 1.00, 1, 0, 1.00, 2, 0, 1.00, 3, 0, 1.00],

                    // Coordinate list of vertex relative display object pivot point (Optional properties, null by default, only available to mesh)
                    // [x0, y0, x1, y1, ...]
                    "vertices": [-64.00, -64.00, 64.00, -64.00, 64.00, 64.00, -64.00, 64.00],

                    // matrix transformation for skin slot registration (Optional properties, null by default, only available to mesh)
                    // [x, y, skewX, skewY, scaleX, scaleY]
                    "slotPose": [0.00, 0.00, 0.0000, 0.0000, 1.0000, 1.0000],

                    // Matrix transformation for skin bone registration (optional attribute default: null, valid only for grid)
                    // [bone index, x, y, skewX, skewY, scaleX, scaleY, ...]
                    "bonePose": [0, 0.00, 0.00, 0.0000, 0.0000, 1.0000, 1.0000],

                    "edges": [0, 1, 1, 2, 2, 3, 3, 1],
                    "userEdges": [],
                }]
            }]
        }],

        // ik Constraint list of this skeleton contains
        "ik": [{

            // ik constraint name
            "name": "ikName",

            // Bound bone name
            "bone": "boneName",

            // Target bone name
            "target": "ikBoneName",

            // Bend direction (Optional properties, true by default)
            // [true: positive direction / clockwise, false: reverse direction / counterclockwise]
            "bendPositive": true,

            // Length of skeleton chain (Optional properties, 0 by default)
            // [0: only constrain bone, n: Constrain bone and bone’s parent bone of up n-level]
            "chain": 0,

            // Weight [0.00: No constraint ~ 1.00: Full constraint] (Optional properties, 0 by default)
            "weight": 1.00
        }],

        // The animations list of this skeleton contains
        "animation": [{

            // animation name
            "name": "animationName",

            // Loop number [0: loop infinitely, n: loop n times] (Optional propertie, 1 by default)
            "playTimes": 1,

            // Animation frame length (Optional properties, 1 by default)
            "duration": 1,

            // Key frame list of this animation contains (Optional properties, null by default)
            "frame": [{

                // Frame length (Optional properties, 1 by default)
                "duration": 1,

                // Frame event (Optional properties, null by default)
                "event": "eventName",

                // Frame sound (Optional properties, null by default)
                "sound": "soundName",

                // Frame behaviors list (Optional properties, null by default)
                "actions": [

                    // This skeleton play specified animation
                    ["gotoAndPlay", "animationName"],

                    // This skeleton play and stop specified animation
                    ["gotoAndStop", "animationName"],
                ]
            }],

            // The skeleton timeline list of this animation contains (Optional properties, null by default)
            "bone": [{

                // Timeline name (corresponding to the bone name)
                "name": "boneName",

                // Timeline zoom (Optional properties, 1.00 by default)
                "scale": 1.00,

                // Timeline offset (Optional properties, 0.00 by default)
                "offset": 0.00,

                // The key frame list of this timeline contains (Optional properties, null by default)
                "frame": [{

                    // Frame length (Optional properties, 1 by default)
                    "duration": 1,

                    // Tween easing [0.00: linear, null: no easing] (optional properties default: null)
                    "tweenEasing": 0.00,

                    // Tween easing curve [x1, y1, x2, y2, ...: Bézier curve] (Optional properties, null by default)
                    "curve": [0.00, 0.00, 1.00, 1.00],

                    // Frame event (Optional properties, null by default)
                    "event": "eventName",

                    // Frame sound (Optional properties, null by default)
                    "sound": "soundName",

                    // Bone’s displacement / bevel / zoom (Optional properties, null by default)
                    "transform": {
                        "x": 0.00, // Horizontal displacement (Optional properties, 0.00 by default)
                        "y": 0.00, // Vertical displacement (Optional properties, 0.00 by default)
                        "skX": 0.0000, // Horizontal chamfer (optional properties, 0.0000 by default)
                        "skY": 0.0000, // Vertical chamfer (optional properties  0.0000 by default)
                        "scX": 1.0000, // horizontal zoom (optional properties, 1.0000 by default)
                        "scY": 1.0000 // Vertical zoom (optional properties, 1.0000 by default)
                    },
                }]
            }],

            // Slot timeline list of this animation contains
            "slot": [{

                // Timeline name (corresponding to slot name)
                "name": "slotName",

                // Key frame list of this timeline contains (Optional properties, null by default)
                "frame": [{

                    // Frame length (Optional properties, 1 by default)
                    "duration": 1,

                    // Tween easing [0.00: linear, null: no easing] (Optional properties, null by default)
                    "tween
                    ": 0.00,

                    // Tween easing curve [x1, y1, x2, y2, ...: Bézier curve] (Optional properties, null by default)
                    "curve": [0.00, 0.00, 1.00, 1.00],

                    // The display object index of this frame (the corresponding slot display object list in the skin) (Optional properties, null by default)
                    "displayIndex": 0,

                    // Color overlay of display object (Optional properties, null by default)
                    "color": {
                        "aM": 100, // Transparency overlay [0~100] (Optional properties, 100 by default)
                        "rM": 100, // red overlay [0~100] (Optional properties, 100 by default)
                        "gM": 100, // green overlay [0~100] (Optional properties, 100 by default)
                        "bM": 100, // blue overlay [0~100] (Optional properties, 100 by default)
                        "aO": 0.00, // Transparent skew [-255~255] (Optional properties, 100 by default)
                        "rO": 0.00, // red skew [-255~255] (Optional properties, 0 by default)
                        "gO": 0.00, // green skew [-255~255] (Optional properties, 100 by default)
                        "bO": 0.00, // blue skew [-255~255] (Optional properties, 100 by default)
                    },

                    // The executed action behavior list when playing current frame (Optional properties, null by default)
                    "actions": [

                        // Sub skeleton play specified animation (only available when display object is skeleton)
                        ["gotoAndPlay", "animationName"],

                        // Sub skeleton play and stop specified animation (only available when display object is skeleton)
                        ["gotoAndStop", "animationName"],
                    ]
                }],
            }],

            // The freeform timeline list that this animation contains (Optional properties, null by default)
            "ffd": [{

                // Timeline name (corresponding to slot name)
                "name": "slotName",

                // Key frame list of this timeline contains (Optional properties, null by default)
                "frame": [{

                    // Frame length (Optional properties, 1 by default)
                    "duration": 1,

                    // Tween easing [0.00: linear, null: no easing] (Optional properties, null by default)
                    "
                    Easing": 0.00,

                    // Tween easing curve control point list [x1, y1, x2, y2, ...: Bézier curve] (Optional properties, null by default)
                    "curve": [0.00, 0.00, 1.00, 1.00],

                    // Vertex coordinate list index offset (Optional properties, 0 by default)
                    "offset": 0,

                    // Vertex coordinate list x0, y0, x1, y1, ...: relative displacement [Optional properties, null by default]
                    "vertices": [0.01, 0.01]
                }]
            }]
        }]
    }]
}
```

------------------------------

# 4.5 Format changes relative to 4.0 version

* Armature
    1. Add the “frameRate” property: able to set a separate frame rate for each skeleton
    2. Add “type” property: bone animation/basic animation/stage animation
    3. Add "defaultActions" list: able to assign default behavior for skeleton (deleted “gotAndPlay” property, and its function are combined with “actions”)
    4. Add “ik” list

* Slot
    1. Add “actions” list: slot is able to assign default behavior for sub-skeleton (deleted “gotAndPlay” property, and its function are combined with “actions” )

* Display
    1."type" property added "mesh" type and other properties that match with it

* Animation
    1. Add “ffd” timeline

* Frame
    1. Add "actions" list: control the sub skeleton behavior (deleted “gotAndPlay” property, and its function are combined with “actions”)

* actions
    Only temporarily support the "gotoAndPlay" behavior, will extend more control behavior and interaction behavior for animation in the future

------------------------------

# 4.0 VS 3.0 format changes

* Armature contains Slot list

* Add skin by default in Skin, and it has features shown as follow:
    1. Rank first in the skin list
    2. Its name is an empty string””
    3. The included slot will exist in other skin at the same time, which is equivalent to saving the slots shared by all other skins (equivalent to the base class for other skins)

* There is no pX, pY properties in the transform property of display of Slot in Skin
    1. Display no longer has the initial pivot point property, and all display pivot points are center points.
    2. Since the pivot point when display is running is the origin of the bone, so the pivot point information here can be converted into the position information of the display during initialization, and the animation can be perfectly restored.

* Changes in Animation
    1. Delete “tweenEasing”: animation will not override keyframe’s easing value
    2. Delete “autoTween”: animation will not override the keyframe’s patch value
    3. "loop" was renamed as "playtime" 
    4. "colorTransform"was renamed as "color"

* Distinguish between Bone timeline and Slot timeline
    1. Bone timeline includes translation, rotation and zoom, custom events and sound events.
    2. Slot timeline includes color changes, displayIndex change and zorder change.

* UserData fields are added to Armature, Bone and Slot, which is used to record user custom info and facilitate third-party extensions.

* Changes in Frame
    1. Remove the hide property, if you want to hide a slot in the animation, setting displayIndex as -1 is the newest operation. And the visible property is completely reserved for developers to dynamically set slot is hidden or not.
    2. Added curve property and use the Bézier curve to describe the easing effect of the animation tween

## 4.0 Data Format Standard Description

<p><span style="-font-family: 宋体,SimSun;">——DragonBones 4.1 still uses the 4.0 data format specification——</span></p><pre class="brush:as3;toolbar:false">{
&nbsp;&nbsp;&quot;name&quot;:&nbsp;&quot;dataName&quot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;DB data name, different DB data files can have a skeleton with the same name, in this case, this field is used to distinguish the data corresponding the skeleton.
&nbsp;&nbsp;&quot;version&quot;:&nbsp;&quot;4.0&quot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;DB version number
&nbsp;&nbsp;&quot;frameRate&quot;:&nbsp;24&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;DB animation frame rate
&nbsp;&nbsp;&quot;isGlobal&quot;:&nbsp;0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】use absolute data or not, 0 by default (use relative data)
&nbsp;&nbsp;&quot;armature&quot;:&nbsp;[{
&nbsp;&nbsp;&nbsp;&nbsp;&quot;name&quot;:&nbsp;&quot;armatureName&quot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Skeleton name, one data file can have multiple skeleton
&nbsp;&nbsp;&nbsp;&nbsp;&quot;userData&quot;:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional property】Custom data area, could be any type, empty by default
&nbsp;&nbsp;&nbsp;&nbsp;&quot;bone&quot;:&nbsp;[{&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;All bone list of skeleton contains
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;name&quot;:&nbsp;&quot;boneName&quot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;bone name
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;parent&quot;:&nbsp;&quot;parentBoneName&quot;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Parent bone name
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;userData&quot;:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】Custom data area, could be any type, empty by default
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;length&quot;:&nbsp;0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】bone length, 0 by default
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;transform&quot;:&nbsp;{x,&nbsp;y,&nbsp;scX,&nbsp;scY,&nbsp;skX,&nbsp;skY}&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Bone’s properties parameters (optional properties)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;x：X-axis coordinate offset, &nbsp;y:&nbsp;Y-axis coordinate offset, 0 by default
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;scX:X-axis scaling value, scY:Y-axis scaling value, 1 by default
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;skX:X-axis rotation value，skY:Y-axis rotation value,&nbsp; 0 by default
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}]
&nbsp;&nbsp;&nbsp;&nbsp;&quot;slot&quot;:&nbsp;[{&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Slot list of skeleton contains
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;name&quot;:&nbsp;&quot;slotName&quot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Slot name
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;parent&quot;:&nbsp;&quot;parentBoneName&quot;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Slot-bound bone
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;userData&quot;:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】Custom data area, could be any type, empty by default
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;displayIndex&quot;:&nbsp;0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】The index of picture list of slot contained of the default picture in the slot, 0 by default.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;blendMode&quot;=&quot;&quot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//Mixed mode, the default value is blank.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}]
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;skin&quot;:&nbsp;[{&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Skin list in the skeleton
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;name&quot;:&nbsp;&quot;skinName&quot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Skin name, the default skin name is &quot;&quot;, contains all shared slot of other skins
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;slot&quot;:&nbsp;[{&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Slot list included in the skin
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;name&quot;:&nbsp;&quot;slotName&quot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;slot name
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;display&quot;:&nbsp;[{&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Display objects list owned in the slot
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;name&quot;:&nbsp;&quot;displayName&quot;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Display object name corresponding to the display object, including the relative path of the secondary directory.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;type&quot;:&nbsp;&quot;image&quot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Display object type, can be image (image), or sub skeleton (armature)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Is able to freely expand based on different engines.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;transform&quot;:&nbsp;{x,&nbsp;y,&nbsp;scX,&nbsp;scY,&nbsp;skX,&nbsp;skY}&nbsp;&nbsp;&nbsp;//&nbsp;Properties parameters of display object (optional properties)，
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;x：X-axis coordinate offset,&nbsp;y:&nbsp;Y-axis coordinate offset，0 by default
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;scX:X-axis scaling value, scY:Y-axis scaling value, 1 by default.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;skX:X-axis rotation value, skY:Y-axis rotation value, &nbsp; 0 by default.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}]
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}]
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}]
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;animation&quot;:&nbsp;[{&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Animation list in skeleton
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;name&quot;:&nbsp;&quot;animationName&quot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;animation name
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;duration&quot;:0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Animation total frame number
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;fadeInTime&quot;:&nbsp;0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】fade-in time, 0 by default.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;scale&quot;:&nbsp;1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】The scaling of animation timeline, 1 by default, the larger the value the longer the play time&nbsp; currently it’s not available in DB&nbsp;Pro.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;playTimes&quot;:&nbsp;1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】Play time, 1 by default, 0 means infinite loop
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;frame&quot;:&nbsp;[{&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Key frame list that animation contains
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;duration&quot;:&nbsp;1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】Key frame’s continuous frame number, 1 by default.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;event&quot;:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】Key frame includes event name, empty by default.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;sound&quot;:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】Key frame includes sound name, empty by default.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;action&quot;:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】Jump action name, empty by default
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}]
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;bone&quot;:&nbsp;[{&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Bone list that animation contains (bone timeline list)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;name&quot;:&nbsp;&quot;boneName&quot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;bone name
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;scale&quot;:&nbsp;1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】Bone timeline scaling value, 1 by default (no scaling)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;offset&quot;:&nbsp;0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】Bone timeline delay [0,&nbsp;1], 0 by default
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;For example, a loop running action has 4 seconds; and the action on the leg is set as 0.25
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Then the leg’s loop is one second ahead of the other bones.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;pX&quot;:&nbsp;0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】0 by default, represents the initial value of the skeleton pivot point in the animation
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;This property only makes sense with the use of data corresponding to Parent
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;If you use relatively global data, this value will be overwritten when the data is parsed.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;pY&quot;:&nbsp;0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】0 by default, represents the initial value of the skeleton pivot point in the animation
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;This property only makes sense with the use of data corresponding to Parent
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;If you use relatively global data, this value will be overwritten when the data is parsed.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;frame&quot;:&nbsp;[{&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Key frame list of bone timeline included
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;duration&quot;:&nbsp;1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】key frame’s continuous frame number, 1 by default.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;tweenEasing&quot;:0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】 It’s easing or not, NaN by default, no easing, 0: linear easing.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;tweenRotate&quot;:0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】Rotate clockwise or counterclockwise for a few rounds, and read from the tween animation. It has to be an integer, and 0 is the default value.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;event&quot;:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】Key frame includes event name, empty by default
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;sound&quot;:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】Key frame includes sound name, empty by default
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;transform&quot;:&nbsp;{x,&nbsp;y,&nbsp;scX,&nbsp;scY,&nbsp;skX,&nbsp;skY}&nbsp;&nbsp;&nbsp;//&nbsp;The property parameters of this frame bone (optional property)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;x：X-axis coordinate offset,&nbsp;y:&nbsp;Y-axis coordinate offset, 0 by default
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;scX:X-axis scaling value, scY:Y-axis scaling value, 1 by default.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;skX:X-axis rotation value, skY:Y-axis rotation value, 0 bye default.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}]
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}]
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;slot&quot;:&nbsp;[{&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Slot list of animation contains (slot timeline list)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;name&quot;:&nbsp;&quot;slotName&quot;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;slot name
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;scale&quot;:&nbsp;1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】slot’s scaling value, 1 by default.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;offset&quot;:&nbsp;0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】Action delay [0,&nbsp;1]，0 by default.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;For example, a loop running action has 4 seconds; and the action on the leg is set as 0.25
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Then the leg’s loop is one second ahead of the other bones.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;frame&quot;:&nbsp;[{&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Key frame list of slot
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;duration&quot;:&nbsp;1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】key frame continuous frame number, 1 by default.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;displayIndex&quot;:0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】This frame displays picture index, 0 by default, -1 means no display.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;Corresponding to picture list index of slot of skin
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;visible&quot;:1&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】Slot is visible or not in this frame, 1 by default.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;zOrder&quot;:&nbsp;0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】The level where the slot is, 0 by default.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;hide&quot;:&nbsp;0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】hide or not, 0 by default (no hidden)
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;tweenEasing&quot;:0&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】 easing or not, NaN by default, no easing, 0: Linear easing.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;action&quot;:&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//【optional properties】 the action of this frame execute, empty by default.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&quot;color&quot;:&nbsp;{aM,&nbsp;rM,&nbsp;gM,&nbsp;bM,&nbsp;aO,&nbsp;rO,&nbsp;gO,&nbsp;bO}&nbsp;//&nbsp;Color overlay. All properties are optional property, and its default value is shown as follow:
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;//&nbsp;The default value of aO,rO,gO,bO are 0, and the default value of aM,rM,gM,bM is 100.
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}]
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}]
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}]
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}]
}</pre><p><br/></p>