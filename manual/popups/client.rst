Popups del Cliente
================

Introducción
------------
Usualmente los usuarios necesitan ver notificaciones de los eventos en el juego.
Este componente, provee unos cuantos tipos de ventana para mostrarle al usuario eventos del juego.

.. image:: images/popups.png

Un ejemplo de esto, es cuando ocurre un evento que afecta directamente el flujo del juego, como un error de
conexión, o simplemente, se solicita que el usuario ingrese un texto para una validación de datos.

Modo de Uso
-----------
El componente de popups es core, es decir que está siempre presente en Brainztorm sin que el usuario pueda encenderlo
o apagarlo. Para el uso de este componente, es necesario crear una instancia de la clase del popup que el usuario
desee mostrar, y mostrarlo a través de la interface *IPopupsDisplayer*, por ejemplo:

.. code-block:: c#

	[Inject]
	private IPopupsDisplayer popUpDisplayer;

	private void ShowSimplePopup()
	{
		SimplePopupData popupData = new SimplePopupData();
		popupData.TitleLabel.Text.SetPlainText("Basic Popup Title");
		popupData.DescriptionLabel.Text.SetPlainText("Basic Popup Description");

		popupData.AcceptButton.IsEnabled = true;
		popupData.AcceptButton.Label.Text.SetPlainText("Accept");

		popupData.DeclineButton.IsEnabled = true;
		popupData.DeclineButton.Label.Text.SetPlainText("Decline");

		popUpDisplayer.OpenOrEnqueue(popupData);
	}

Este fragmento de código dará como resultado un popup como este:

.. image:: images/basic_popup_example.png

El usuario también puede crear sus propios popups personalizados y modificar el skin de los que
ofrece el SDK desde el editor. Para crear popups personalizados, el usuario puede crear una clase
que herede de la clase SimplePopup, y un controlador para el tipo de popup que se debe añadir al
gameobject del popup que el usuario acaba de crear, de la siguiente manera:

.. code-block:: c#

  public class ExamplePopupData : SimplePopupData
  {
    //
  }

  public class ErrorReportPopupHandler : PopupDataHandlerBase<ExamplePopupData>
  {
      protected override void Setup (ExamplePopupData popupData)
      {
          base.Setup (popupData);
      }
  }

  Una vez creado el popup, al momento de agregar el controlador, esté añadira automaticamente los
  componentes *Popup* y *BackNavigationObject* los cuales son importantes para la navegación de las
  ventanas. Acto seguido el prefab debe agregarse a la lista de popups de Brainztorm que están
  disponibles en el juego:

  .. image:: images/popup_prefabs_settings.png

  Componentes de los Popups
  -------------------------

Para construir los popups, es necesario hacerlo teniendo en cuenta los siguientes componentes
que provee el SDK:

PopUpLabelData.cs
^^^^^^^^^^^^^^^^^
Campo de texto estático dentro del popup, puede activarse o desactivarse mediante el campo *IsEnabled*,
Su texto puede ser un valor localizado o un texto estático, el cual puede asignarse mediante los
métodos *Text.SetLocalizationKey (string localizationKey, params object[] replacements)* o
*Text.SetPlainText (string plainText, params object[] replacements)*.

Su controlador es *PopupLabel.cs* y es el script que se debe agregar al componente de texto de
Unity (UnityEngine.UI.Text) que quiere representar el Label dentro del popup.

.. code-block:: c#

	[Serializable]
	public class PopupLabelData
	{
		[SerializeField]
		private bool isEnabled = true;

		[SerializeField]
		private BrainztormString text = new BrainztormString();

		public bool IsEnabled
		{
			get { return isEnabled; }
			set { isEnabled = value; }
		}

		public BrainztormString Text
		{
			get { return text; }
			set { text = value; }
		}
	}

	[RequireComponent(typeof(Text))]
	[DisallowMultipleComponent]
	public class PopupLabel : MonoBehaviour
	{
		public void Setup(PopupLabelData data)
		{
      //
		}
	}

PopupInputFieldData.cs
^^^^^^^^^^^^^^^^^^^^^^
Componente de texto que el usuario ingresa por pantalla, al igual que el componente
PopupLabelData, este puede activarse o desactivarse desde la propiedad *IsEnabled*,
sin embargo, este posee dos propiedades PopupLabelData, uno es el componente *FieldText*,
que es el texto que el usuario ingresa desde el controlador, y la propiedad *Placeholder*,
que es la marca de agua que se muestra en el campo de texto cuando este está vacío.

Su controlador es *PopupInputField.cs* y es el script que se debe agregar al componente de input de
Unity (UnityEngine.UI.InputField) que quiera representar el campo de texto dentro del popup.

.. code-block:: c#

	[Serializable]
	public class PopupInputFieldData
	{
		[SerializeField]
		private bool isEnabled = true;

		[SerializeField]
		private PopupLabelData fieldText = new PopupLabelData();

		[SerializeField]
		private PopupLabelData placeHolder = new PopupLabelData();

		public bool IsEnabled
		{
			get { return isEnabled; }
			set { isEnabled = value; }
		}

		public PopupLabelData FieldText
		{
			get { return fieldText; }
		}

		public PopupLabelData Placeholder
		{
			get { return placeHolder; }
		}
	}

  [RequireComponent(typeof(Text))]
  [DisallowMultipleComponent]
  public class PopupInputField : MonoBehaviour
  {
		[SerializeField]
		private PopupLabel placeHolder;

		[SerializeField]
		private PopupLabel inputFieldText;

		[SerializeField]
		private bool autoSelect = true;

    public void Setup(PopupInputFieldData data)
    {
			placeHolder.Setup(data.Placeholder);
			inputFieldText.Setup(data.FieldText);
    }
  }

PopupButtonData.cs
^^^^^^^^^^^^^^^^^^^^^^
Componente de tipo botón, como los demás componentes, puede habilitarse o inhabilitarse desde la propiedad
*IsEnabled*, además de esto, posee una propiedad PopupLabelData, que es el texto que contiene el botón, y una propiedad
llamada *PresCallback*, un evento de tipo Action, que es la acción que se efectuará al presionar el botón; la propiedad
*ClosePopupOnPress*, tiene la función de cerrar o no el popup cuando el botón sea presionado.

Su controlador es *PopupButton.cs* y es el script que se debe agregar al componente de botón de
Unity (UnityEngine.UI.Button) que quiere representar el botón dentro del popup.

.. code-block:: c#

    [Serializable]
    public class PopupButtonData
    {
        [SerializeField]
        private bool isEnabled = true;
        [SerializeField]
        private bool closePopupOnPress = true;
        [SerializeField]
        private PopupLabelData label = new PopupLabelData ();

        public Action PressCallback;

        public bool IsEnabled
        {
            get { return isEnabled; }
            set { isEnabled = value; }
        }

        public bool ClosePopupOnPress
        {
            get { return closePopupOnPress; }
            set { closePopupOnPress = value; }
        }

        public PopupLabelData Label
        {
            get { return label; }
        }
    }

    [RequireComponent (typeof (Button))]
    [DisallowMultipleComponent]
    public class PopupButton : MonoBehaviour
    {
        [SerializeField]
        private PopupLabel label;

        private Button button;

        public void Setup (PopupButtonData data, Action close)
        {
            gameObject.SetActive (data.IsEnabled);
            SetupOnClick (data, close);
            SetupLabel (data);
        }

        private void SetupOnClick (PopupButtonData data, Action close)
        {
          //
        }

        private void SetupLabel (PopupButtonData data)
        {
          //
        }
    }
