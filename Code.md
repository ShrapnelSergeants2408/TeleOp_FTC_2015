# TeleOp_FTC_2015
The TeleOp code for FTC 2015


package com.qualcomm.ftcrobotcontroller.opmodes;

    import com.qualcomm.robotcore.eventloop.opmode.OpMode;
    import com.qualcomm.robotcore.hardware.DcMotor;
    import com.qualcomm.robotcore.hardware.Servo;

    public class FixedOp extends OpMode {

        DcMotor Left;
        DcMotor Right;
        DcMotor Intake1;
        DcMotor Convey1;

        Servo BallTilt;

        double convey_power;
        double intake_power;

        public FixedOp() {

        }

        @Override
        public void init() {
            Right = hardwareMap.dcMotor.get("Right");
            Left = hardwareMap.dcMotor.get("Left");
            Intake1 = hardwareMap.dcMotor.get("Intake1");
            Convey1 = hardwareMap.dcMotor.get("Convey1");
            BallTilt = hardwareMap.servo.get("BallTilt");
        }

        @Override
        public void loop() {
            float left = -gamepad1.left_stick_y;
            float right = gamepad1.right_stick_y;

            if (gamepad1.b) {
                left = -left;
                right = -right;
            }

            if (gamepad1.a) {
                left = left * (.5f);
                right = right * (.5f);
            }

            Right.setPower(right);
            Left.setPower(left);

            convey_power = 0;
            if (gamepad2.right_bumper) {
                convey_power = .9;
            }
            if (gamepad2.left_bumper) {
                convey_power = -.9;
            }
            Convey1.setPower(convey_power);


            intake_power = 0;

            if (gamepad2.y) {
                intake_power = .85;
            }
            if (gamepad2.a) {
                intake_power = -.85;
            }
            Intake1.setPower(intake_power);

            BallTilt.setPosition(.45f);
            if (gamepad2.x) {
                BallTilt.setPosition(.53f);
            }
            if (gamepad2.b) {
                BallTilt.setPosition(.37f);
            }
        }
    }
