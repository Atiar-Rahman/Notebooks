```js
import React from 'react';
import Lottie from "react-lottie";
import Lanimation from '../data/loaing-animation.json';

const Loading = () => {
    const defaultOptions = {
        loop: true,
        autoplay: true,
        animationData: Lanimation,
        rendererSettings: {
            preserveAspectRatio: "xMidYMid slice"
        }
    };

    return (
        <div className="flex items-center justify-center h-screen">
            <Lottie options={defaultOptions} height={200} width={200} />
        </div>
    );
};

export default Loading;

```

