# How to Create a Custom Switchboard Device Plugin

**Source:** [https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-create-a-custom-switchboard-device-plugin-for-unreal-engine](https://dev.epicgames.com/documentation/en-us/unreal-engine/how-to-create-a-custom-switchboard-device-plugin-for-unreal-engine)  
**Processed:** 2025-06-14 16:28:48

---

Depending on your project's needs and the devices you are using, you may need to add or extend the device functionality in [Switchboard](/documentation/en-us/unreal-engine/switchboard-in-unreal-engine). This page covers creating your own device plugin in Python. With some C++ knowledge, it is possible to extend the listener to accept more types of messages but this is not covered here.

The following instructions step through how to create a new device plugin, **SampleDevice**, for Switchboard that you can use as a starting point.

1.  For the device plugin to be discoverable on load in Switchboard, you must create a folder and Python file with the naming convention `<plugin_name>\plugin_<plugin_name>.py` in `\Engine\Plugins\VirtualProduction\Switchboard\Source\Switchboard\switchboard\devices\`.
    -   For the **SampleDevice** plugin create the following file: `\Engine\Plugins\VirtualProduction\Switchboard\Source\Switchboard\switchboard\devices\sampledevice\plugin_sampledevice.py`.
2.  Extend the `Device`class defined in `\Engine\Plugins\VirtualProduction\Switchboard\Source\Switchboard\switchboard\devices\device_base.py` in the `plugin_sampledevice.py` file:
    
    -   Import `Device` from `device_base.py`.
    -   Create a new class `DeviceSampleDevice` which inherits from `Device`.
    -   Import `LOGGER` from `switchboard/switchboard_logging.py` to report errors.
        
        ```
        		
              ``from switchboard.devices.device_base import Device       from switchboard.switchboard_logging import LOGGER        class DeviceSampleDevice(Device):`           def __init__(self, name, ip_address, **kwargs):           super().__init__(name, ip_address, **kwargs)``
        			
        Copy full snippet
        ```
        from switchboard.devices.device\_base import Device from switchboard.switchboard\_logging import LOGGER class DeviceSampleDevice(Device):\` def \_\_init\_\_(self, name, ip\_address, \*\*kwargs): super().\_\_init\_\_(name, ip\_address, \*\*kwargs)
    
    Verify the file is discoverable by Switchboard. Launch Switchboard and expand the **Add Device** dropdown menu. **SampleDevice** appears in the list.
    
    ![Adding your custom device to Switchboard](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/1d1cd76f-8e3e-4018-af90-b5a77a38b726/switchboard_add_custom_device_1.png)
3.  Adding a SampleDevice to your Switchboard won't create a widget in the view. To create a SampleDevice widget, extend `DeviceWidget` in `plugin_sampledevice.py`:
    
    -   Import `DeviceWidget` from `device_widget_base.py`.
    -   Create the new class `DeviceWidgetSampleDevice` which inherits from `DeviceWidget`.
        
        ```
        					
                  `from switchboard.devices.device_base import Device           from switchboard.devices.device_widget_base import DeviceWidget           from switchboard.switchboard_logging import LOGGER 			           class DeviceSampleDevice(Device):               def __init__(self, name, ip_address, **kwargs):                   super().__init__(name, ip_address, **kwargs) 			           class DeviceWidgetSampleDevice(DeviceWidget):               def __init__(self, name, device_hash, ip_address, icons, parent=None):                   super().__init__(name, device_hash, ip_address, icons, parent=parent)`
        								
        Copy full snippet
        ```
        from switchboard.devices.device\_base import Device from switchboard.devices.device\_widget\_base import DeviceWidget from switchboard.switchboard\_logging import LOGGER class DeviceSampleDevice(Device): def \_\_init\_\_(self, name, ip\_address, \*\*kwargs): super().\_\_init\_\_(name, ip\_address, \*\*kwargs) class DeviceWidgetSampleDevice(DeviceWidget): def \_\_init\_\_(self, name, device\_hash, ip\_address, icons, parent=None): super().\_\_init\_\_(name, device\_hash, ip\_address, icons, parent=parent)
    
    Verify the widget appears in Switchboard. Launch Switchboard and add a SampleDevice. A minimal SampleDevice widget appears in the view.
    
    ![Switchboard custom device widget](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/5266c847-cf07-46b7-8ba0-316cf790e350/switchboard_add_custom_device_2.png)
4.  Create a custom dialog when a new SampleDevice is added by creating a new class which inherits from `AddDeviceDialog` and assigning it to the static variable `add_device_dialog` in the `DeviceSampleDevice` class:
    
    -   Import `AddDeviceDialog` from `device_widget_base.py`.
    -   Import Qt modules from PySide2
    -   Create a new class `AddSampleDeviceDialog` which inherits from `AddDeviceDialog` and set the device\_type parameter to "SampleDevice" when calling the base class's constructor.
    -   In the new class's constructor add a QLineEdit text field to the dialog.
    -   Override the `add_device_dialog` static variable in `DeviceSampleDevice` with the new class.
        
        ```
        					
                  `from switchboard.devices.device_base import Device           from switchboard.devices.device_widget_base import AddDeviceDialog, DeviceWidget           from switchboard.switchboard_logging import LOGGER 			           from PySide2 import QtWidgets, QtGui, QtCore 			           class AddSampleDeviceDialog(AddDeviceDialog):               def __init__(self, existing_devices, parent=None):                   super().__init__(device_type="SampleDevice", existing_devices=existing_devices, parent=parent) 			                   # Create QTWidgets to add to the form                   self.additional_text_field = QtWidgets.QLineEdit(self) 			                   # Append the new options to the QTWidgets.QFormLayout object defined in the parent class                   self.form_layout.addRow("Additional Text", self.additional_text_field) 			           class DeviceSampleDevice(Device):               # Override the add device dialog object associated with the device plugin               add_device_dialog = AddSampleDeviceDialog 			               def __init__(self, name, ip_address, **kwargs):                   super().__init__(name, ip_address, **kwargs) 			           class DeviceWidgetSampleDevice(DeviceWidget):               def __init__(self, name, device_hash, ip_address, icons, parent=None):                   super().__init__(name, device_hash, ip_address, icons, parent=parent)`
        			
        Copy full snippet
        ```
        from switchboard.devices.device\_base import Device from switchboard.devices.device\_widget\_base import AddDeviceDialog, DeviceWidget from switchboard.switchboard\_logging import LOGGER from PySide2 import QtWidgets, QtGui, QtCore class AddSampleDeviceDialog(AddDeviceDialog): def \_\_init\_\_(self, existing\_devices, parent=None): super().\_\_init\_\_(device\_type="SampleDevice", existing\_devices=existing\_devices, parent=parent) # Create QTWidgets to add to the form self.additional\_text\_field = QtWidgets.QLineEdit(self) # Append the new options to the QTWidgets.QFormLayout object defined in the parent class self.form\_layout.addRow("Additional Text", self.additional\_text\_field) class DeviceSampleDevice(Device): # Override the add device dialog object associated with the device plugin add\_device\_dialog = AddSampleDeviceDialog def \_\_init\_\_(self, name, ip\_address, \*\*kwargs): super().\_\_init\_\_(name, ip\_address, \*\*kwargs) class DeviceWidgetSampleDevice(DeviceWidget): def \_\_init\_\_(self, name, device\_hash, ip\_address, icons, parent=None): super().\_\_init\_\_(name, device\_hash, ip\_address, icons, parent=parent)
    
    Verify the new device dialog appears in Switchboard. Launch Switchboard and add a SampleDevice. The additional text field appears in the dialog.
    
    ![Switchboard adding custom device dialog](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f43a5ef9-9611-46d5-b5f9-5c1d71e6b314/switchboard_add_custom_device_3.png)
5.  Devices can also have a widget on the right side of Switchboard, tabbed with other extension dialogs, to share more information. To create this tab, override the classmethod `plug_into_ui` from the `Device` base class.
    
    -   Create a new class `SampleDeviceTabView` which inherits from `QtWidgets.QWidget`.
    -   Create the class member `tab_view` in `DeviceSampleDevice` to hold the instance of the widget.
    -   Override the classmethod `plug_into_ui` in `DeviceSampleDevice` and initialize `tab_view` with the new class `SampleDeviceTabView`.
        
        ```
        					
                  `from switchboard.devices.device_base import Device           from switchboard.devices.device_widget_base import AddDeviceDialog, DeviceWidget           from switchboard.switchboard_logging import LOGGER 			           from PySide2 import QtWidgets, QtGui, QtCore 			           class AddSampleDeviceDialog(AddDeviceDialog):               def __init__(self, existing_devices, parent=None):                   super().__init__(device_type="SampleDevice", existing_devices=existing_devices, parent=parent) 			                   # Create QTWidgets to add to the form                   self.additional_text_field = QtWidgets.QLineEdit(self) 			                   # Append the new options to the QTWidgets.QFormLayout self.form_layout object defined in the parent class                   self.form_layout.addRow("Additional Text", self.additional_text_field) 			           class DeviceSampleDevice(Device):               add_device_dialog = AddSampleDeviceDialog # Override the default dialog for the plugin               tab_view = None 			               def __init__(self, name, ip_address, **kwargs):                   super().__init__(name, ip_address, **kwargs) 			               @classmethod               def plug_into_ui(cls, menubar, tabs):                   ''' Implementation of base class function that allows plugin to inject UI elements.                   ''' 			                   if not cls.tab_view:                       cls.tab_view = SampleDeviceTabView(parent=tabs) 			                   tabs.addTab(cls.tab_view, 'SampleDevice Tab') 			           class DeviceWidgetSampleDevice(DeviceWidget):               def __init__(self, name, device_hash, ip_address, icons, parent=None):                   super().__init__(name, device_hash, ip_address, icons, parent=parent) 			           class SampleDeviceTabView(QtWidgets.QWidget):               def __init__(self, parent):                   QtWidgets.QWidget.__init__(self, parent)`
        								
        Copy full snippet
        ```
        from switchboard.devices.device\_base import Device from switchboard.devices.device\_widget\_base import AddDeviceDialog, DeviceWidget from switchboard.switchboard\_logging import LOGGER from PySide2 import QtWidgets, QtGui, QtCore class AddSampleDeviceDialog(AddDeviceDialog): def \_\_init\_\_(self, existing\_devices, parent=None): super().\_\_init\_\_(device\_type="SampleDevice", existing\_devices=existing\_devices, parent=parent) # Create QTWidgets to add to the form self.additional\_text\_field = QtWidgets.QLineEdit(self) # Append the new options to the QTWidgets.QFormLayout self.form\_layout object defined in the parent class self.form\_layout.addRow("Additional Text", self.additional\_text\_field) class DeviceSampleDevice(Device): add\_device\_dialog = AddSampleDeviceDialog # Override the default dialog for the plugin tab\_view = None def \_\_init\_\_(self, name, ip\_address, \*\*kwargs): super().\_\_init\_\_(name, ip\_address, \*\*kwargs) @classmethod def plug\_into\_ui(cls, menubar, tabs): ''' Implementation of base class function that allows plugin to inject UI elements. ''' if not cls.tab\_view: cls.tab\_view = SampleDeviceTabView(parent=tabs) tabs.addTab(cls.tab\_view, 'SampleDevice Tab') class DeviceWidgetSampleDevice(DeviceWidget): def \_\_init\_\_(self, name, device\_hash, ip\_address, icons, parent=None): super().\_\_init\_\_(name, device\_hash, ip\_address, icons, parent=parent) class SampleDeviceTabView(QtWidgets.QWidget): def \_\_init\_\_(self, parent): QtWidgets.QWidget.\_\_init\_\_(self, parent)
    
    ![Custom device added to Switchboard](https://d1iv7db44yhgxn.cloudfront.net/documentation/images/f08337c9-c193-4d7f-bcba-3e8b71145926/switchboard_add_custom_device_4.png)

These steps showed how to create a new device plugin for Switchboard. For an advanced example, see the nDisplay device plugin for Switchboard.