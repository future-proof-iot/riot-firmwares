# name of your application
APPLICATION = dashboard_riot_a8_m3

# Use IoT-LAB board:
BOARD = iotlab-a8-m3

# This has to be the absolute path to the RIOT base directory:
RIOTBASE ?= $(CURDIR)/../../RIOT

# Riot Application modules
USEMODULE += printf_float
USEMODULE += lsm303dlhc
USEMODULE += shell_common

# Include pyaiot modules
USEMODULE += coap_common
USEMODULE += coap_utils
USEMODULE += coap_led
USEMODULE += coap_position
USEMODULE += coap_iotlab_a8_m3

# Change this to 0 show compiler invocation lines by default:
QUIET ?= 1

# Needed because of unuesed variuable in stm32_common/perip/i2c_2.c
# Fixed in Master but waiting for 2019.04-branch release that has the
# bug fix
DEVELHELP ?= 1

# Application specific definitions and includes
APPLICATION_NAME ?= "IoT-Lab\ A8\ Node"
NODE_LAT ?= 48.714784
NODE_LNG ?= 2.205502
# CoAP broker server information
BROKER_ADDR ?= 2001:660:3207:102::4
BROKER_PORT ?= 5683

include $(CURDIR)/../Makefile.dep
include $(CURDIR)/../Makefile.include

include $(RIOTBASE)/Makefile.include

CFLAGS += -DBROKER_ADDR=\"$(BROKER_ADDR)\"
CFLAGS += -DBROKER_PORT=$(BROKER_PORT)
CFLAGS += -DAPPLICATION_NAME="\"$(APPLICATION_NAME)\""
CFLAGS += -DNODE_LAT=\"$(NODE_LAT)\"
CFLAGS += -DNODE_LNG=\"$(NODE_LNG)\"

# Set a custom channel if needed
ifneq (,$(filter cc110x,$(USEMODULE)))          # radio is cc110x sub-GHz
  DEFAULT_CHANNEL ?= 0
  CFLAGS += -DCC110X_DEFAULT_CHANNEL=$(DEFAULT_CHANNEL)
else
  ifneq (,$(filter at86rf212b,$(USEMODULE)))    # radio is IEEE 802.15.4 sub-GHz
    DEFAULT_CHANNEL ?= 5
    FLAGS += -DIEEE802154_DEFAULT_SUBGHZ_CHANNEL=$(DEFAULT_CHANNEL)
  else                                          # radio is IEEE 802.15.4 2.4 GHz
    DEFAULT_CHANNEL ?= 26
    CFLAGS += -DIEEE802154_DEFAULT_CHANNEL=$(DEFAULT_CHANNEL)
  endif
endif
