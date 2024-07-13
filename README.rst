========================
pibooth-picture-template
========================

|PythonVersions| |PypiPackage| |Downloads|

``pibooth-picture-template``, `pibooth`_ uygulaması için bir eklentidir.

Bu eklenti, **çekimlerin/metinlerin konumlarını ve boyutlarını** bir şablon kullanarak tanımlamaya olanak tanır. Şablon dosyası (XML, `mxGraphModel tanımı <https://jgraph.github.io/mxgraph/docs/tutorial.html>`_ temelinde) ücretsiz çevrimiçi diyagram yazılımı `Flowchart Maker`_ kullanılarak kolayca oluşturulabilir/düzenlenebilir. 

.. image:: https://github.com/pibooth/pibooth-picture-template/blob/master/docs/images/FlowchartMaker.png?raw=true
   :align: center
   :width: 500
   :alt: Flowchart Maker
   :target: https://app.diagrams.net

Bir dizi şablon `GitHub <https://github.com/pibooth/pibooth-picture-template/tree/master/templates>`_ üzerinde bulunabilir.

Bu eklenti tarafından otomatik olarak yüklenen `fancy.xml <https://github.com/pibooth/pibooth-picture-template/blob/master/templates/fancy.xml?raw=true>`_
şablonu ``~/.config/pibooth/picture_template.xml`` dizinine kaydedilir.

Aşağıda, bu şablonla oluşturulan resimler bulunmaktadır (burada nasıl `Bir şablon oluşturulur`_ öğreneceksiniz):

+---------------------------------------+---------------------------------------+
|          |fancy1_landscape|           |          |fancy3_landscape|           |
+---------------------------------------+---------------------------------------+
|          |fancy2_landscape|           |          |fancy4_landscape|           |
+-------------------+-------------------+-------------------+-------------------+

+-------------------+-------------------+-------------------+-------------------+
| |fancy1_portrait| | |fancy2_portrait| | |fancy3_portrait| | |fancy4_portrait| |
+-------------------+-------------------+-------------------+-------------------+

Kurulum
-------

::

    $ pip3 install pibooth-picture-template

Yapılandırma
-------------

Aşağıda `pibooth`_ yapılandırmasında kullanılabilen yeni yapılandırma seçenekleri bulunmaktadır.
**Anahtarlar ve varsayılan değerleri, ilk** `pibooth`_ **yeniden başlatmadan sonra otomatik olarak yapılandırmanıza eklenir.**

.. code-block:: ini

    [PICTURE]

    # Resim şablonu yolu, 8 sayfa (4 çekim numarası ve 2 yön) içermelidir
    template = picture_template.xml

.. note:: Yapılandırmayı düzenlemek için ``pibooth --config`` komutunu çalıştırın.

Resim İşleme
-------------

Yalnızca **çekimler**, **metinler** ve **resimler**in konum/boyutu işlenir. Bu, şablona ek olarak, nihai resmi oluşturmak için aşağıdaki yapılandırma anahtarlarının da dikkate alındığı anlamına gelir:

* ``[PICTURE][footer_text1]``
* ``[PICTURE][footer_text2]``
* ``[PICTURE][text_colors]``
* ``[PICTURE][text_fonts]``
* ``[PICTURE][text_alignments]``
* ``[PICTURE][overlays]``
* ``[PICTURE][backgrounds]``

Resim Yönlendirme
-----------------

Seçilen çekim numarası için istenen yön şablon dosyasında bulunamazsa bir ``TemplateParserError`` hatası oluşturulur.

Eğer ``[PICTURE][orientation] = auto`` ise, en iyi yönlendirme şu kurallara göre seçilir:

* Doğru sayıda çekim ve yer tutucuya sahip aynı yönlendirme ile bir şablon bulun.
* Doğru sayıda çekime sahip bir şablon bulun.
* Dikey yönlendirmeye sahip bir şablon bulun.

Bir Şablon Oluşturma
--------------------

Aşağıdaki adımlar, `Flowchart Maker`_ uygulamasını kullanarak sıfırdan temel bir şablon dosyasının nasıl oluşturulacağını gösterecektir.

Bu dosya, ``1`` / ``2`` / ``3`` / ``4`` çekim ve ``dikey`` / ``yatay`` yönlendirmeleri için resim düzenini tanımlamak üzere birkaç şablon içerebilir.

Adım 1: Yeni bir dosya oluşturma
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

===========  ==================================================================
 |step1_1|   ``Yeni Diyagram Oluştur``a tıklayın.

 |step1_2|   Boş bir diyagram seçin. Diyagramın adını değiştirin, bu dışa aktarılacak
             dosyanın adı olacaktır. ``Oluştur``a tıklayın.

 |step1_3|   Uygun kağıt boyutunu seçin. Özel bir boyut *inç* olarak tanımlanabilir.
===========  ==================================================================

.. note:: Var olan bir dosyadan başlamak daha kolay olabilir. ``Mevcut Diyagramı Aç``a tıklayın
          ve ``~/.config/pibooth/picture_template.xml`` dizininde bulunan varsayılan şablon dosyasını yükleyin.

Adım 2: Çekim yer tutucu
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

===========  ==================================================================
 |step2_1|   Bir çekim yer tutucu tanımlamak için bir dikdörtgen seçin. Diğer şekiller
             etkisiz olacaktır ve dikdörtgen olarak kabul edilir.

 |step2_2|   Dikdörtgeni istenen boyuta uyacak şekilde yeniden boyutlandırın. Dikdörtgen
             sayfa sınırını aşabilir, tasarım efektleri oluşturmak için kullanılabilir. En fazla 4
             dikdörtgen çizilebilir.

 |step2_3|   Çekim yer tutucuları numaralandırılmalıdır (``1`` ila ``4``) yerleştirilecek çekimleri
             tanımlamak için. Renklendirilmiş şekiller düzen hakkında daha iyi bir genel bakış sağlar ancak
             nihai resimde render edilmezler.
===========  ==================================================================

.. note:: Şablona resimler de eklenebilir. Görüntüleme sırasını seçmek için ``Arkaya Gönder``
          veya ``Öne Gönder`` seçeneklerini kullanın (PNG ve JPG formatları kabul edilir).

Adım 3: Metin yer tutucu
^^^^^^^^^^^^^^^^^^^^^^^^

===========  ==================================================================
 |step3_1|   Bir metin yer tutucu temsil etmek için bir metin kutusu seçin.

 |step3_2|   Metin kutusunu istenen boyuta uyacak şekilde yeniden boyutlandırın. `pibooth`
             yapılandırmasına bağlı olarak en fazla 2 metin kutusu çizilebilir.

 |step3_3|   Metin yer tutucuları numaralandırılmalıdır (``1``, ``2``,
             ``footer_text1`` veya ``footer_text2``) yerleştirilecek metni tanımlamak için.
===========  ==================================================================

Adım 4: Resim çözünürlüğü
^^^^^^^^^^^^^^^^^^^^^^^^^^

===========  ==================================================================
 |step4_1|   Şablona ekstra özellikler eklenebilir. Kağıt boyutu ayarlarının
             yakınındaki ``Verileri Düzenle`` düğmesine tıklayın. Giriş kutusuna
             ``dpi`` yazın ve ``Özellik Ekle``ye tıklayın.

 |step4_2|   Varsayılan olarak ``600`` DPI çözünürlüğü kullanılır. Bu, resim boyutunun
             4x6 inç çözünürlüğünde 2400x3600 piksel olacağı anlamına gelir. İstenen
             değeri ayarlayın ve ``Uygula``ya tıklayın.
===========  ==================================================================

Adım 5: Yeni bir şablon ekleme
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

===========  ==================================================================
 |step5_1|   Şablon oluşturulduktan sonra, başka bir çekim sayısı veya başka bir
             yönlendirme için yeni bir şablon tanımlanabilir. Yeni bir sayfa
             eklemek için ``+``ya tıklayın.

 |step5_2|   Aynı resim şablonda birkaç kez kullanılabilir, simetrik bir şablon
             oluşturmak için (bir kopya sizin için, bir kopya misafirleriniz için).
===========  ==================================================================

Adım 6: Şablon dosyasını kaydetme
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

===========  ==================================================================
 |step6_1|   XML dosyasını oluşturmak için ``Dosya``, ``Farklı Dışa Aktar``,
             ``XML...``a tıklayın.

 |step6_2|   ``Sıkıştırılmış``ı seçmeyi kaldırın, dosyayı manuel olarak düzenlemek
             isterseniz. ``Dışa Aktar``a tıklayın.
===========  ==================================================================

.. note:: Şablonunuzun sonucunu test etmek için her seferinde `pibooth`_ çalıştırmak yerine,
          ``pibooth-regen`` komutunu kullanın. Bu komut, yeni şablonu kullanarak ``~/Pictures/pibooth`` dizininde bulunan
          mevcut resimleri yeniden oluşturacaktır.


.. --- Bağlantılar ------------------------------------------------------------------

.. _`pibooth`: https://pypi.org/project/pibooth

.. _`Flowchart Maker`: https://app.diagrams.net

.. |PythonVersions| image:: https://img.shields.io/badge/python-3.6+-red.svg
   :target: https://www.python.org/downloads
   :alt: Python 3.6+

.. |PypiPackage| image:: https://badge.fury.io/py/pibooth-picture-template.svg
   :target: https://pypi.org/project/pibooth-picture-template
   :alt: PyPi paketi

.. |Downloads| image:: https://img.shields.io/pypi/dm/pibooth-picture-template?color=purple
   :target: https://pypi.org/project/pibooth-picture-template
   :alt: PyPi indirmeleri

.. --- Örnekler ---------------------------------------------------------------

.. |fancy1_landscape| image:: https://github.com/pibooth/pibooth-picture-template/blob/master/docs/examples/fancy1_landscape.jpg?raw=true
   :width: 90 %
   :align: middle
   :alt: fancy1_landscape

.. |fancy2_landscape| image:: https://github.com/pibooth/pibooth-picture-template/blob/master/docs/examples/fancy2_landscape.jpg?raw=true
   :width: 90 %
   :align: middle
   :alt: fancy2_landscape

.. |fancy3_landscape| image:: https://github.com/pibooth/pibooth-picture-template/blob/master/docs/examples/fancy3_landscape.jpg?raw=true
   :width: 90 %
   :align: middle
   :alt: fancy3_landscape

.. |fancy4_landscape| image:: https://github.com/pibooth/pibooth-picture-template/blob/master/docs/examples/fancy4_landscape.jpg?raw=true
   :width: 90 %
   :align: middle
   :alt: fancy4_landscape

.. |fancy1_portrait| image:: https://github.com/pibooth/pibooth-picture-template/blob/master/docs/examples/fancy1_portrait.jpg?raw=true
   :width: 90 %
   :align: middle
   :alt: fancy1_portrait

.. |fancy2_portrait| image:: https://github.com/pibooth/pibooth-picture-template/blob/master/docs/examples/fancy2_portrait.jpg?raw=true
   :width: 90 %
   :align: middle
   :alt: fancy2_portrait

.. |fancy3_portrait| image:: https://github.com/pibooth/pibooth-picture-template/blob/master/docs/examples/fancy3_portrait.jpg?raw=true
   :width: 90 %
   :align: middle
   :alt: fancy3_portrait

.. |fancy4_portrait| image:: https://github.com/pibooth/pibooth-picture-template/blob/master/docs/examples/fancy4_portrait.jpg?raw=true
   :width: 90 %
   :align: middle
   :alt: fancy4_portrait

.. --- Eğitim ---------------------------------------------------------------

.. |step1_1| image:: https://github.com/pibooth/pibooth-picture-template/blob/master/docs/images/step1_1_create.png?raw=true
   :width: 80 %
   :alt: step1_1_create

.. |step1_2| image:: https://github.com/pibooth/pibooth-picture-template/blob/master/docs/images/step1_2_blank.png?raw=true
   :width: 80 %
   :alt: step1_2_blank

.. |step1_3| image:: https://github.com/pibooth/pibooth-picture-template/blob/master/docs/images/step1_3_size.png?raw=true
   :width: 80 %
   :alt: step1_3_size

.. |step2_1| image:: https://github.com/pibooth/pibooth-picture-template/blob/master/docs/images/step2_1_rectangle.png?raw=true
   :width: 80 %
   :alt: step2_1_rectangle

.. |step2_2| image:: https://github.com/pibooth/pibooth-picture-template/blob/master/docs/images/step2_2_rectangle_resize.png?raw=true
   :width: 80 %
   :alt: step2_2_rectangle_resize

.. |step2_3| image:: https://github.com/pibooth/pibooth-picture-template/blob/master/docs/images/step2_3_numbering.png?raw=true
   :width: 80 %
   :alt: step2_3_numbering

.. |step3_1| image:: https://github.com/pibooth/pibooth-picture-template/blob/master/docs/images/step3_1_text.png?raw=true
   :width: 80 %
   :alt: step3_1_text

.. |step3_2| image:: https://github.com/pibooth/pibooth-picture-template/blob/master/docs/images/step3_2_text_resize.png?raw=true
   :width: 80 %
   :alt: step3_2_text_resize

.. |step4_1| image:: https://github.com/pibooth/pibooth-picture-template/blob/master/docs/images/step4_1_property.png?raw=true
   :width: 80 %
   :alt: step4_1_property

.. |step4_2| image:: https://github.com/pibooth/pibooth-picture-template/blob/master/docs/images/step4_2_dpi.png?raw=true
   :width: 80 %
   :alt: step4_2_dpi

.. |step5_1| image:: https://github.com/pibooth/pibooth-picture-template/blob/master/docs/images/step5_1_new_template.png?raw=true
   :width: 80 %
   :alt: step5_1_new_template

.. |step5_2| image:: https://github.com/pibooth/pibooth-picture-template/blob/master/docs/images/step5_2_symetric.jpg?raw=true
   :width: 80 %
   :alt: step5_2_symetric

.. |step6_1| image:: https://github.com/pibooth/pibooth-picture-template/blob/master/docs/images/step6_1_xml.png?raw=true
   :width: 80 %
   :alt: step6_1_xml

.. |step6_2| image:: https://github.com/pibooth/pibooth-picture-template/blob/master/docs/images/step6_2_export.png?raw=true
   :width: 80 %
   :alt: step6_2_export
