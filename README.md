# Unity Tweening
A simple script that allows complex tweening animations in Unity.

## Basic Use
The Tween class contains a collection of static methods for tweening multiple data types.
For example, `Tween.DoTween(Color.black, Color.white, 2f, delegate (Color c) { spriteRenderer.color = c; });`
</br>Be sure to include the *DavidFDev* namespace to obtain access to my tweening script.

All methods begin with *DoTween* and take in the following arguments:
- **startValue**: Initial value of the tween.
- **endValue**: Destination value of the tween.
- **duration**: Time, in seconds, that it takes for the tween to animate fully.
- **onUpdate**: Action to invoke each time the tween value updates (every frame).
- **easingFunction**: Easing function to use, that will change how the animation plays out.
- **onFinished**: Action to invoke when the tween has animated fully.

Extension methods can further simplify the method.
</br>For example, `transform.TweenPositionY(0f, 10f, 2f);`

## Easing Functions
Easing functions can be used to change how the animation plays out. There are a variety of easing functions included in my script, which are abstracted under the *EasingFunction* enum.

For example, `audioSource.TweenVolume(0f, 1f, 1f, EasingFunction.EASE_IN_OUT_SINE);`

Check out visualisations of easing functions at [https://easings.net/](https://easings.net/).

## Tween Instance
Every tween method returns a *TweenRef* instance, which is a class that contains information about the tween.
For example, `TweenRef<Vector2> tweenScale = transform.TweenScale2D(transform.localScale, transform.localScale * 1.5f, 0.75f, EasingFunction.SPIKE);`

The *TweenRef* instance can be paused, stopped, or played at any time.
```
if (tweenScale.Running)
  tweenScale.StopTween();
```

Furthermore, a *TweenRef* instance can be instantiated at any time using the *new* keyword.
For example, `TweenRef<float> myTween = new TweenRef<float>(0f, 100f, 5f, Mathf.Lerp, delegate (float f) { Debug.Log(f); }, EasingFunction.EASE_OUT_BOUNCE);`
However, instantiating an instance will require you to supply an appropriate lerping function, such as *Mathf.Lerp*.

## Methods List
- **DoTween**: Tween a float, Vector2, Vector3, Color, Quaternion, or other type.
- **DoTweenAngle**: Tween an angle, using *Mathf.LerpAngle*.
- **DoTweenProperty**: Tween a property on a Unity object using reflection.
- **DoTweenPropertyAngle**: Tween a property on a Unity object using reflection, using *Mathf.LerpAngle*.
- **DoTweenInstance**: Begin tweening an instance of *TweenRef*.

## Extensions List
### Transform
- **TweenPositionX** | **TweenPositionY** | **TweenPositionZ**
- **TweenPosition2D** | **TweenPosition3D**
- **TweenLocalPosition2D** | **TweenLocalPosition3D**
- **TweenRotationX** | **TweenRotationY** | **TweenRotationZ**
- **TweenRotation** | **TweenLocalRotation**
- **TweenQuaternion** | **TweenLocalQuaternion**
- **TweenScale2D** | **TweenScale3D**

### RectTransform
- **TweenAnchoredPosition**

### AudioSource
- **TweenVolume**
- **TweenPitch**

### Graphic (Image, RawImage, Text, etc.)
- **TweenColour**
- **TweenAlpha**

### SpriteRenderer
- **TweenColour**
- **TweenAlpha**

### Light
- **TweenColour**
- **TweenIntensity**

### Camera
- **TweenOrthographicSize**
- **TweenFOV**
