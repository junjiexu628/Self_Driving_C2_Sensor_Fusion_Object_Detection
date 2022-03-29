# Self_Driving_C2_Sensor_Fusion_Object_Detection

## 1, Write a short recap of the four tracking steps and what you implemented there (EKF, track management, data association, camera-lidar sensor fusion). Which results did you achieve? Which part of the project was most difficult for you to complete, and why?
- Step 1: Extended Kalman filter

Create the prediction and measurement update functions. The prediction function includes two parts to focus on, one is the F() function for motion model(such as constant velocity model for our project work), the other is Q() function for the process estimation error covariance.

The measurement function is a bit complex, including gamma(), S() and K(). The residual estimation error covariance R is defined by the pre-set parameters. They are different for Lidar and camera.

get_H() function is also necessary part for the measurement update, and it is from the Measurement class.

- Step2: Track management

intialize the track state as track.x and track.P based on the measurement class. Set the track state as three situations: initialized, tentative and confirmed by the track.score.

Delete the track by the delete_track function and update the track list.

The functions of manage_track(), delete_track(), handle_update_track() need to be created.

- Step3: Data association

The MDH() function is defined for calculating the Mahalanobis distance of the track and measurement.Also the gating threshold is used for excluding these high MHD pairs. The minimum value of pair can be found and update the unassigned track and measurement list. Utill the data assocaitaion matrix is inf, no pairs are left.

- Step4: Camera sensor fusion
- 
Activate the camera detection by implement the in_fov() function to check the object in the vision of the sensor, and initialize the camera Z,R parameters.Finish the get_hx() functon for camera nonlinear measurement definition.

I think the overall structure of this sensor fusion is most difficult for me. Every separate part is clear, but how to integrate them into one is not easy for me. This project is suitable to understand the the whole process and all task is covered by the course.

## 2, Do you see any benefits in camera-lidar fusion compared to lidar-only tracking (in theory and in your concrete results)?
In theory the camera has high resolution, better on the detection, espacially in the day light environment. Camera performs well on the traffic light, and traffic signs, even the lanes lines on the road for measuring the color characteristic. These advantage are unique for the camera in comparison of the Lidar. 

Lidar provides the precise the spatial coordinate of the objects and more accurate distance information of the objects. Even more the Lidar performs very well in the dark night scene.

The camera-lidar fusion is better than the any single sensor on the overall detection and track performance. They combine their advantage and result in low RMSE than the only Lidar tracking results. Although our project doesn't make the best RMSE result due to the default parameter, the benefit of sensor fusion is definitely.

## 3, Which challenges will a sensor fusion system face in real-life scenarios? Did you see any of these challenges in the project?
Our sensor fusion system could face the real-life issues. 

Because the scenario in the project is pre-defined in the day light condition, but the reality is all conditions involved in dark, rain, tensive light and so on. 
The process noise and measurement noise variance is fixed for this specific situation. In reality the noise variance should be adapted for all situation.

In the real world scenario, the association of track and measurememnt should be accurate, so the gating threshold is the key to the association in the all conditions.

## 4,Can you think of ways to improve your tracking results in the future?
- Fine-tune the parameterization and see how low an RMSE can be achieved. One idea would be to apply the standard deviation values for lidar that found in the mid-term project. 
- Implement a more advanced data association, e.g. Global Nearest Neighbor (GNN) or Joint Probabilistic Data Association (JPDA).
- Adapt the Kalman filter to also estimate the object's width, length, and height, instead of simply using the unfiltered lidar detections as we did.
- Use a non-linear motion model, e.g. a bicycle model, which is more appropriate for vehicle movement than our linear motion model.
 
