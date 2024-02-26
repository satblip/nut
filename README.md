# Network UPS Tools server

Docker image for Network UPS Tools server version 2.8.1 for Legrand UPS.

## Usage

This image provides a complete UPS monitoring service (USB driver only).

Start the container:

```console
# docker run \
	--name nut \
	--detach \
	--publish 3493:3493 \
	--device /dev/bus/usb/xxx/yyy \
  -v ./config/ups.conf:/etc/nut/ups.conf \
  -v ./config/upsd.conf:/etc/nut/upsd.conf \
  -v ./config/upsd.users:/etc/nut/upsd.users \
  -v ./config/upsmon.conf:/etc/nut/upsmon.conf \
	satblip/nut
```

## Configuration via configuration files

This image needs to be configured via the file that you can find in the `config` directory.
Token are in place in those files, here are the values you need to replace:

### UPS_NAME

*Example value*: `ups`

The name of the UPS.

### UPS_DESC

*Example value*: `Eaton 5SC`

This allows you to set a brief description that upsd will provide to clients that ask for a list of connected equipment.

### UPS_DRIVER

*Example value*: `usbhid-ups`

This specifies which program will be monitoring this UPS.

### UPS_PORT

*Example value*: `auto`

This is the serial port where the UPS is connected.

### API_USER

*Example value*: `upsmon`

This is the username used for communication between upsmon and upsd processes.

### API_PASSWORD

*Example value*: `secret`

This is the password for the upsmon user.

### SHUTDOWN_CMD

*Example value*: `echo 'System shutdown not configured!'`

This is the command upsmon will run when the system needs to be brought down. The command will be run from inside the container.

