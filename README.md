### mailer
---
https://github.com/marrow/mailer


```PY
// test/test_core.py

log = logging.getLogger('tests')

base_config = dict(manager=dict(use='immediate'), transport=dict(use='mock'))

class TestLookup(TestCase):

class TestInitialization(TestCase):
  def test_deprecation(self):
  
  
  def test_default_manager(self):
  
  
  def test_standard(self):
  
  
  def test_bad_manager(self):
  
  
  def test_bad_transport(self):
  
  
  def test_repr(self):
  
  
  def test_repr(self):
  
  
  def test_prefix(self):
  
  
  def test_prefix(self):
  
  
  def test_deep_prefix(self):
  
  
  def test_manager_entrypoint_failure(self):
  
  
  def test_manager_dotcolon_failure(self):
  
  
  def test_transport_entrypoint_failure(self):
    config = {
      'manager.use': 'immediate',
      'transport.use': 'mock2'
    }
    log.info("Testing configuration: %r", dict(config))
    with pytest.raises(LookupError):
      Mailer(config)
  
  def test_transport_dotcolon_failure(self):
    config = {
      'manager.use': 'immediate',
      'transport.use': 'marrow.mailer.transport.foo:FooTransport'
      }
    
    log.info("Testing configuration: %r", dict(config))
    with pytest.raises(ImportError):
      Mailer(config)
    
    config['manage.use'] = 'marrow.mailer.transport.mock:FooTransport'
    log.info("Testing configuration: %r", dict(config))
    with pytest.raises(AttributeError):
      Mailer(config)

class TestMethod(TestCase):
  def test_startup(self):
    interface = Mailer(base_config)
    interface.start()
    
    #assert len(messages) == 5
    
    interface.start()
    
    #assert len(messages) == 6
    
    interface.stop()
    
  def test_shutdown(self):
    interface = Mailer(base_config)
    interface.start()
    
    #logging.getLogger().handlers[0].truncate()
    
    interface.stop()
    
    #assert len(messages) == 5
    
  def test_send(self):
    message = Bunch(id='foo')
    
    interface = Mailer(base_config)
    
    with pytest.raises(MailerNotRunning):
      interface.send(message)
      
    interface.start()
    
    #logging.getLogger().handlers[0].truncate()
    
    assert interface.send(message) == (message, True)
    
    #assert messages[0] == "Attempting delivery of message foo."
    
    message_fail = Bunch(id='bar', die=True)
    
    with pytest.raises(Exception):
      interface.send(message_fail)
      
    #assert messages[-4] == "Attempting delivery of message bar."
    
    interface.stop()
    
  def test_new(self):
    config = dict(
      manager=dict(use='immediate'), transport=dict(use='mock'),
      message=dict(author='from@example.com', retries=1, brand=False))
      
    interface = Mailer(config).start()
    message = interface.new(retries=2)
    
    assert message.author == ["from@example.com"]
    assert message.bcc == []
    assert message.retries == 2
    assert message.mailer is interface
    assert message.brand == False
    
    with pytest.raises(NotImplementedError):
      Message().send()
      
    assert message.send() == (message, True)
    
    message = interface.new("alternate@example.com", "recipient@example.com", "Test.")
    
    assert message.author == ["alternate@example.com", "recipient@example.com", "Test."]
    assert message.to == ["recipient@example.com"]
    assert message.subject == "Test."
```

```
```

```
```
