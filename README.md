# intern-documentation
Links and code samples.


## JavaScript inheritance patterns
[Crockford, inheritance example](https://stackoverflow.com/questions/2709612/using-object-create-instead-of-new)
```javascript
window.Quad = (function() {

    function Quad() {

        const wheels = 4;
        const drivingWheels = 2;

        let motorSize = 0;

        function setMotorSize(_) {
            motorSize = _;
        }

        function getMotorSize() {
            return motorSize;
        }

        function getWheelCount() {
            return wheels;
        }

        function getDrivingWheelCount() {
            return drivingWheels;
        }
        return Object.freeze({
            getWheelCount,
            getDrivingWheelCount,
            getMotorSize,
            setMotorSize
        });
    }

    return Object.freeze(Quad);
})();

window.Car4wd = (function() {

    function Car4wd() {
        const quad = new Quad();

        const spareWheels = 1;
        const extraDrivingWheels = 2;

        function getSpareWheelCount() {
            return spareWheels;
        }

        function getDrivingWheelCount() {
            return quad.getDrivingWheelCount() + extraDrivingWheels;
        }

        return Object.freeze(Object.assign({}, quad, {
            getSpareWheelCount,
            getDrivingWheelCount
        }));
    }

    return Object.freeze(Car4wd);
})();

let myQuad = new Quad();
let myCar = new Car4wd();
console.log(myQuad.getWheelCount()); // 4
console.log(myQuad.getDrivingWheelCount()); // 2
console.log(myCar.getWheelCount()); // 4
console.log(myCar.getDrivingWheelCount()); // 4 - The overridden method is called
console.log(myCar.getSpareWheelCount()); // 1
```
