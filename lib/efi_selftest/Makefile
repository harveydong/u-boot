# SPDX-License-Identifier: GPL-2.0+
#
# (C) Copyright 2017, Heinrich Schuchardt <xypron.glpk@gmx.de>

# This file only gets included with CONFIG_EFI_LOADER set, so all
# object inclusion implicitly depends on it

CFLAGS_efi_selftest_miniapp_exit.o := $(CFLAGS_EFI) -Os -ffreestanding
CFLAGS_REMOVE_efi_selftest_miniapp_exit.o := $(CFLAGS_NON_EFI)
CFLAGS_efi_selftest_miniapp_return.o := $(CFLAGS_EFI) -Os -ffreestanding
CFLAGS_REMOVE_efi_selftest_miniapp_return.o := $(CFLAGS_NON_EFI)

obj-y += \
efi_selftest.o \
efi_selftest_bitblt.o \
efi_selftest_config_table.o \
efi_selftest_controllers.o \
efi_selftest_console.o \
efi_selftest_crc32.o \
efi_selftest_devicepath_util.o \
efi_selftest_events.o \
efi_selftest_event_groups.o \
efi_selftest_exception.o \
efi_selftest_exitbootservices.o \
efi_selftest_gop.o \
efi_selftest_loaded_image.o \
efi_selftest_manageprotocols.o \
efi_selftest_memory.o \
efi_selftest_register_notify.o \
efi_selftest_rtc.o \
efi_selftest_snp.o \
efi_selftest_textinput.o \
efi_selftest_textinputex.o \
efi_selftest_textoutput.o \
efi_selftest_tpl.o \
efi_selftest_util.o \
efi_selftest_variables.o \
efi_selftest_watchdog.o

obj-$(CONFIG_EFI_DEVICE_PATH_TO_TEXT) += efi_selftest_devicepath.o
obj-$(CONFIG_EFI_UNICODE_COLLATION_PROTOCOL) += efi_selftest_unicode_collation.o

obj-$(CONFIG_CPU_V7) += efi_selftest_unaligned.o
obj-$(CONFIG_EFI_LOADER_HII) += efi_selftest_hii.o

ifeq ($(CONFIG_GENERATE_ACPI_TABLE),)
obj-y += efi_selftest_fdt.o
endif

ifeq ($(CONFIG_BLK)$(CONFIG_PARTITIONS),yy)
obj-y += efi_selftest_block_device.o
endif

# TODO: As of v2019.01 the relocation code for the EFI application cannot
# be built on ARMv7-M, Sandbox, and x86_64.
ifeq ($(CONFIG_SANDBOX)$(CONFIG_CPU_V7M)$(CONFIG_X86_64),)

obj-y += \
efi_selftest_loadimage.o \
efi_selftest_startimage_exit.o \
efi_selftest_startimage_return.o

targets += \
efi_miniapp_file_image_exit.h \
efi_miniapp_file_image_return.h \
efi_selftest_miniapp_exit.efi \
efi_selftest_miniapp_return.efi

$(obj)/efi_miniapp_file_image_exit.h: $(obj)/efi_selftest_miniapp_exit.efi
	$(obj)/../../tools/file2include $(obj)/efi_selftest_miniapp_exit.efi > \
	$(obj)/efi_miniapp_file_image_exit.h

$(obj)/efi_miniapp_file_image_return.h: $(obj)/efi_selftest_miniapp_return.efi
	$(obj)/../../tools/file2include $(obj)/efi_selftest_miniapp_return.efi > \
	$(obj)/efi_miniapp_file_image_return.h

$(obj)/efi_selftest_loadimage.o: $(obj)/efi_miniapp_file_image_exit.h

$(obj)/efi_selftest_startimage_exit.o: $(obj)/efi_miniapp_file_image_exit.h

$(obj)/efi_selftest_startimage_return.o: $(obj)/efi_miniapp_file_image_return.h

endif
