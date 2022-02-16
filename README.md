using System.Collections;
using System.Collections.Generic;
using UnityEngine;

public class CarDriver : MonoBehaviour
{
    public Transform wheel_front_right_transform;
    public Transform wheel_front_left_transform;
    public Transform wheel_back_right_transform;
    public Transform wheel_back_left_transform;

    [Space(10)]


    public WheelCollider wheel_front_right;
    public WheelCollider wheel_front_left;
    public WheelCollider wheel_back_right;
    public WheelCollider wheel_back_left;

    [Space(10)]

    public float wheelTorque;
    public float brakeTorque;


    private void FixedUpdate()
    {
        if (Input.GetKey(KeyCode.W))
        {
            DriveForward();

        }
        if (Input.GetKey(KeyCode.S))
        {
            DriveBack();
        }
        if (Input.GetKey(KeyCode.D))
        {
            TurnRight();
        }
        if (Input.GetKeyUp(KeyCode.D))
        {
            ResetWheelRotation();
        }

        if (Input.GetKey(KeyCode.A))
        {
            TurnLeft();
        }
        if (Input.GetKeyUp(KeyCode.A))
        {
            ResetWheelRotation();
        }
        if (Input.GetKey(KeyCode.Space))
        {
            Stop();
        }

        ApplyWheelRotation(wheel_front_right, wheel_front_right_transform);
        ApplyWheelRotation(wheel_front_left, wheel_front_left_transform);
        ApplyWheelRotation(wheel_back_right, wheel_back_right_transform);
        ApplyWheelRotation(wheel_back_left, wheel_back_left_transform);


    }



    private void DriveForward()
    {
        wheel_front_right.motorTorque = wheelTorque;
        wheel_front_left.motorTorque = wheelTorque;
        wheel_back_right.motorTorque = wheelTorque;
        wheel_back_left.motorTorque = wheelTorque;

        wheel_front_right.brakeTorque = 0;
        wheel_front_left.brakeTorque = 0;
        wheel_back_right.brakeTorque = 0;
        wheel_back_left.brakeTorque = 0;


    }

    private void DriveBack()
    {
        wheel_front_right.motorTorque = -wheelTorque;
        wheel_front_left.motorTorque = -wheelTorque;
        wheel_back_right.motorTorque = -wheelTorque;
        wheel_back_left.motorTorque = -wheelTorque;

        wheel_front_right.brakeTorque = 0;
        wheel_front_left.brakeTorque = 0;
        wheel_back_right.brakeTorque = 0;
        wheel_front_left.brakeTorque = 0;
    }

    private void TurnRight()
    {
        wheel_front_right.steerAngle = 30;
        wheel_front_left.steerAngle = 30;
    }

    private void TurnLeft()
    {
        wheel_front_right.steerAngle = -30;
        wheel_front_left.steerAngle = -30;
    }

    private void ResetWheelRotation()
    {
        wheel_front_right.steerAngle = 0;
        wheel_front_left.steerAngle = 0;
    }

    private void Stop()
    {
        wheel_front_right.brakeTorque = brakeTorque;
        wheel_front_left.brakeTorque = brakeTorque;
        wheel_back_right.brakeTorque = brakeTorque;
        wheel_back_left.brakeTorque = brakeTorque;
    }

    private void ApplyWheelRotation(WheelCollider wheelCollider, Transform wheelTransform)
    {
        Vector3 position;
        Quaternion rotation;

        wheelCollider.GetWorldPose(out position, out rotation);

        wheelTransform.position = position;
        wheelTransform.rotation = rotation;

    }

}
