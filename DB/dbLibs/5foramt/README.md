
```javascript
{
    // DragonBones data name
    "name": "dragonBonesName",

    // data version
    "version": "5.0",
    
    // compatible version
    "compatibleVersion": "4.5",

    // animation frame rate
    "frameRate": 24,

    // Custom data (optional property, null by default)
    "userData": null,

    // skeleton list
    "armature": [{

        // Skeleton name (one DragonBones data can contain multiple skeleton)
        "name": "armatureName",

        // Animation frame rate (optional property, use global frame rate by default)
        "frameRate": 24,

        // Animation type (optional property, "Armature" by default)
        // ["Armature": skeleton animation, "MovieClip": basic animation, "Stage": stage animation]
        "type": "Armature",


        // Custom data (optional property, null by default)
        "userData": null,

        // Behavior list that’s added to the back of stage (optional property, null by default)
        "defaultActions": [

            // This skeleton plays specified animation
            ["gotoAndPlay", "animationName"],

            // This skeleton plays and stops specified animation
            ["gotoAndStop", "animationName"],
        ],

        // Bone list of this skeleton contains
        "bone": [{

            // bone name
            "name": "boneName",

            // parent bone name
            "parent": "parentBoneName",

            // Custom data [any type] (optional property, null by default)
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
                "aM": 100, // Transparent overlay [0~100] (Optional properties default: 100)
                "rM": 100, // red overlay [0~100] (Optional properties default: 100)
                "gM": 100, // green overlay [0~100] (Optional properties default: 100)
                "bM": 100, // blue overlay [0~100] (Optional properties default: 100)
                "aO": 0.00, // Transparent skew [-255~255] (Optional properties default: 0)
                "rO": 0.00, // red skew [-255~255] (Optional properties
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

                    // Skeleton name of sub skeleton point to, map name of mesh contains (optional property, null by default, only available to sub skeleton and mesh)
                    "path": "path",

                    // Index of shared mesh (optional property, null by default, only available to mesh)
                    "share": "meshName",

                    // If inherit animation or not (optional property, true by default, only available to shared mesh)
                    "inheritFFD": true,

                    // Bound box type (optional property, rectangle by default, only available to bound box)
                    // ["rectangle": rectangle, "ellipse": ellipse, "polygon": Custom polygon]
                    "subType": "rectangle", 

                    // Display object color (optional property, 0 by default, only available to bound box)
                    "color": 0,

                    // Display object displacement/chamfer/zoom relative to bone (optional properties default: null)
                    "transform": {
                        "x": 0.00, // horizontal displacement (Optional properties, 0.00 by default)
                        "y": 0.00, // y vertical displacement (Optional properties, 0.00 by default)
                        "skX": 0.0000, // Horizontal chamfer (Optional properties, 0.0000 by default)
                        "skY": 0.0000, // Vertical chamfer (Optional properties, 0.0000 by default)
                        "scX": 1.0000, // Vertical zoom (optional properties, 1.0000 by default)
                        "scY": 1.0000, // Vertical zoom (optional properties, 1.0000 by default)
                    },

                    // Pivot point of display object (Optional properties, null by default, no available to sekleton)
                    "pivot": {
                        "x": 0.50, // horizontal pivot point [0.00~1.00] (Optional properties, 0.50 by default)
                        "y": 0.50, // vertical pivot point [0.00~1.00] (Optional properties, 0.50 by default)
                    },

                    // Width and height of rectangle or ellipse (Optional properties, 0 by default, only available to bound box)，
                    "width": 100, "height": 100,

                    // Coordinate list of the vertex relative to the display object pivot point (optional property, null by default, only available to mesh or custom polygon bound box)
                    // [x0, y0, x1, y1, ...]
                    "vertices": [-64.00, -64.00, 64.00, -64.00, 64.00, 64.00, -64.00, 64.00],

                    // Vertex UV coordinate list (Optional properties, null by default, only available to mesh)
                    // [u0, v0, u1, v1, ...]
                    "uvs": [0.0000, 0.0000, 1.0000, 0.0000, 1.0000, 1.0000, 0.0000, 1.0000],

                    // Triangle vertex index list (Optional properties, null by default, only available to mesh)
                    "triangles": [0, 1, 2, 2, 3, 0],

                    // Vertex weight list (Optional properties, null by default, only available to mesh)
                    // [Bone number, bone index, weight, ..., ...]
                    "weights": [1, 0, 1.00, 2, 0, 0.50, 1, 0.50],

                    // matrix transformation for skin slot registration (Optional properties, null by default, only available to mesh)
                    // [a, b, c, d, tx, ty]
                    "slotPose": [1.0000, 0.0000, 0.0000, 1.0000, 0.00, 0.00],

                    // Matrix transformation for skin bone registration (optional attribute default: null, valid only for grid)
                    // [bone index, a, b, c, d, tx, ty, ...]
                    "bonePose": [0, 1.0000, 0.0000, 0.0000, 1.0000, 0.00, 0.00]
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

            //  Weight [0.00: No constraint ~ 1.00: Full constraint] (Optional properties, 0 by default)
            "weight": 1.00
        }],

        // The animations list of this skeleton contains
        "animation": [{

            // animation name
            "name": "animationName",

            // Loop number [0: loop infinitely, n: loop n times] (Optional propertie, 1 by deDisplay object colorimes": 1,

            // Animation frame length (Optional properties, 1 by default)
            "duration": 1,

            // Key frame list of this animation contains (Optional properties, null by default)
            "frame": [{

                // Frame length (Optional properties, 1 by default)
                "duration": 1,

                // Frame sound (Optional properties, null by default)
                "sound": "soundName",

                // Frame behaviors list (Optional properties, null by default)
                "events": [{

                    // event name
                    "name": "eventName",

                    // bone name (Optional properties, null by default)
                    "bone": "boneName",

                    // Slot name (Optional properties, null by default)
                    "slot": "slotName",

                    // Event parameter list (Optional properties, null by default)
                    "ints":[0， 1， 2],
                    "floats":[0.01， 1.01， 2.01],
                    "strings":["a", "b", "c"]
                }],

                // Frame behavior list (Optional properties, null by default)
                "actions": [

                    // This skeleton play specified animation
                    ["gotoAndPlay", "animationName"],

                    // This skeleton play an stop specified animation
                    ["gotoAndStop", "animationName"],
                ]
            }],

            // Depth order timeline
            "zOrder": {
                "frame": [{
                    
                    // frame length (Optional properties,1 by default)
                    "duration": 1,

                    // slot offset [slotIndexA, offsetA, slotIndexB, offsetB, ...] (Optional properties, null by default)
                    "zOrder": [0, 2, 4, 1, 6, -1]
                }]
            },

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

                    //Easing type [0: use tweenEasing or curve to describe easing type, 1~N: Other extension easing type enumeration (about the details of enumeration we will define it in the future)] Optional properties, 0 by default
                    "tweenType": 0,

                    // Easing value [0.00: linear, null: no easing]( Optional properties, null by default)
                    "tweenEasing": 0.00,

                    // Bezier curve easing parameter list [x1, y1, x2, y2, ...] (optional properties, null by default)
                    "curve": [0.00, 0.00, 1.00, 1.00],

                    // Bone displacement/ bevel / scaling (Optional properties, null by default)
                    "transform": {
                        "x": 0.00, // Horizontal displacement (Optional properties, 0.00 by default)
                        "y": 0.00, // Vertical displacement (Optional properties, 0.00 by default)
                        "skX": 0.0000, //  Horizontal chamfer (optional properties, 0.0000 by default)
                        "skY": 0.0000, // Vertical chamfer (optional properties  0.0000 by default)
                        "scX": 1.0000, //  horizontal zoom (optional properties, 1.0000 by default)
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

                    // Easing type [0: use tweenEasing to describe easing type, N: Other extension easing type] Optional properties, 0 by default
                    "tweenType": 0,

                    // Tween easing [0.00: linear, null: no easing] (Optional properties, null by default)
                    "tweenEasing": 0.00,

                    // Tween easing Bezier curve [x1, y1, x2, y2, ...] (Optional properties, null by default)
                    "curve": [0.00, 0.00, 1.00, 1.00],

                    // The display object index of this frame (the corresponding slot display object list in the skin) (Optional properties,0 by default)
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

                // Timeline name
                "name": "timelineName",
                
                // skin name
                "skin": "skinName",

                // slot name
                "slot": "slotName",

                // Key frame list of this timeline contains (Optional properties, null by default)
                "frame": [{

                    // Frame length (Optional properties, 1 by default)
                    "duration": 1,

                    // Easing type [0: use tweenEasing to describe easing type, N: Other extension easing type] Optional properties, 0 by default
                    "tweenType": 0,

                    // Tween easing [0.00: linear, null: no easing] (Optional properties, null by default)
                    "tweenEasing": 0.00,

                    // Tween easing Bezier curve [x1, y1, x2, y2, ...] (Optional properties, null by default)
                    "curve": [0.00, 0.00, 1.00, 1.00],

                    // Vertex coordinate list index offset (Optional properties, null by default)
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
# 5.0 Format changes relative to [4.5](DragonBones_4.5_data_format_zh.md) 

## Root
* Add "compatibleVersion" property.
* Delete "isGlobal" property
	* It does not support absolute coordinate any more, only support relative coordinate, equal to set isGlobal as 0.
	* The case where isGlobal is 1 (absolute coordinates) only exists in the data format using 2.3 and previous version.
	* It supports relative coordinates starting from 3.0 version, so introducing isGlobal property is used for backward compatibility, while it supports relative and absolute coordinates at the same time.
	* It does not support absolute coordinates from 5.0 any more.

## Display
* Add “path” property, which is distinguished from name, and is used to identify the texture path pointed to by the image, the texture path contained in the Mesh, or the pointed skeleton name by the sub-skeleton.
* The meaning of the name property changed to the unique identifier of the display, and does not represent the path anymore.

## Support bound box
* The value of the "type" property of "display" added "boundingBox", used for marking the bound box.  
* The display of bound box type contain properties shown as below:
	* "subType": mark the bound box types, possible values are "rectangle": rectangle, "ellipse": ellipse, "polygon": custom polygon
	* "width", "height": width and height（Only available to rectangle or ellipse type’s bound box）
	* "vertices": vertex list (only available to bound box of custom polygon type)

## Support shared mesh（Linked Mesh）
* Display of mesh type adds "share" property, we can set share property to change it as shared mesh.
* The shared mesh can control it inherits the FED animation of the main mesh via "inheritFFD" property or not.

## Support display order change of slot in animation (ZOrder)
* Add “zOrder” property in "animation", represent the depth order timeline
* "zOrder" contains the frames property, which represents the keyframe list on the timeline. Each keyframe object included contains the following properties:
	* "duration": keyframe’s duration length.
	* "zOrder": on this keyframe, zOrder needs an array consisted of changing slot and changing magnitude.

## Events are thrown by the main timeline unified, supporting multiple event and event parameter lists.
* Delete event property of keyframe contained in bone timeline. (When version update, the date will be moved to the keyframe at the same position of the main timeline)
* The “ frame" of "animation" (the keyframe list contained in the main timeline) contained keyframe data’s event property, changed as “events”, represents the event list that needs to be thrown on that frame.
* Event object contains the properties shown as follow:
	* "name": event name
	* "bone": the bone that throws the event, null by default (the event that the original bone contained will record the bone name here)
	* The slot that throw the event, null by default (this property and the aforementioned bone property cannot exist at the same time, if they do not exist, which means event thrown by the skeleton)
	* "ints": Shape parameter list
	* "floats": float parameter list
	* "strings": String parameter list

## Add more easing type definitions
* Add "tweenType" property to keyframe data that “frame” contains
* "tweenType", 0 by default, represent that tweenEasing or curve to describe easing type (same with 4.5 version)
* "tweenType" is not 0, represent using enumerations of other extension easing types, and the exact meaning of each enumeration will be defined in the future.
