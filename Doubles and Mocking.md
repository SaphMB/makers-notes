# Doubles and Mocking

Instead of creating an instance of an outside class whilst testing a class in spec, doubles a allow us to create dummy of that class instance. Whilst instances of a class can be used as test objects within the tests of another class, this can raise some issues wth one being lack of isolation.

Say, we have a Bakery class as well as a Cake class, and the Bakery class has class methods that interact with instances of the cakes. When testing these methods, if instances of Cake are created when testing the bakery class, it is dependant on the Cake class and could be affected by changes to the Cake class. As its tests strive to test a single component, that component being dependent on another component means that the unit tests may not test what they aim to test.

```shell
describe ‘bakery’ do
    it 'raises an error when full' do
      subject.capacity.times { subject.bake Cake.new }
      expect { subject.bakery Cake.new }.to raise_error ‘Mits away! We’re over-caked!’
    end
  end
```

This test could utilised an instance double of cake as opposed to creating capita number of instances. Instance doubles are the most common type of verifying double. They take a class name or object as the first argument, then verifies that any methods being stubbed would be present on an instance of that class. In addition, when it receives messages, it verifies that the provided arguments are supported by the method signature. The above could be:
```shell
   let(:cake) { double :cake }
```
...
```shell
describe 'dock' do
  it 'raises an error when full' do
    subject.capacity.times { subject.bake double :cake }
    expect { subject.bake double(:cake) }.to raise_error 'Mits away! We’re over-caked!'
  end
end
```
A replacement with the minimum functionality needed


Can use a fake object or a double

e.g.

```shell
#bakery_spec

class FakeCake

	def iced?
		true
	end

end
```

```shell
   let(:cake) { double :cake , dock: false}
```
>explicitly saying that dock respond to false

Is equal to ^^

Should not need to ‘require’ more than one class in the spec
Should not need more than one subject

Read about Kernel

```shell
def stormy? #the class being tested, need to test both outcomes
	rand(6) < 5
end

describe ‘Weather’ do
  context ‘stormy’ do
    it ‘returns true’ do
      allow(Kernel).to receive(:rand) {5} #stubbing the rand method
      expect(subject.stormy?) to eq true #Kernel no essential here
    end
  end
end

describe ‘Weather’ do
  context ‘stormy’ do
    it ‘returns false’ to
      allow(Kernel).to receive(:rand) {5} #stubbing the rand method
      expect(subject.stormy?) to eq true #Kernel no essential here
    end
  end
end
```

Look up:
Allow blocks
Before blocks
Context blocks
Let blocks
